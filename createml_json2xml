## labelimg createml json to labelimg pascal voc xml
import os
from tqdm import tqdm
 
from read_json import ReadAnno
from create_xml_anno import CreateAnno
 
 
def json_transform_xml(json_path, xml_path):
    json_path = json_path
    json_data = json.load(open(json_path))
    filename=json_data[0]['image']
    coordis=[]
    for single_shape in json_data[0]['annotations']:
            # print(single_shape)
            bbox_class = single_shape['label']
            x = single_shape['coordinates']['x']
            y = single_shape['coordinates']['y']
            w = single_shape['coordinates']['width']
            h = single_shape['coordinates']['height']
            xmin= (2*x-w)/2
            xmax= (2*x+w)/2
            ymin= (2*y-h)/2
            ymax= (2*y+h)/2
            coordis.append([xmin,ymin,xmax,ymax,bbox_class])
    print(coordis)
    xml_anno = CreateAnno()
    xml_anno.add_filename(filename)
    xml_anno.add_pic_size(width_text_str=str(1280), height_text_str=str(720), depth_text_str=str(3))
    # print(width)
    for xmin,ymin,xmax,ymax,label in coordis:
        # print(xmin,ymin,xmax,ymax,label)
        xml_anno.add_object(name_text_str=str(label),
                            xmin_text_str=str(int(xmin)),
                            ymin_text_str=str(int(ymin)),
                            xmax_text_str=str(int(xmax)),
                            ymax_text_str=str(int(ymax)))
 
    xml_anno.save_doc(xml_path)
 
if __name__ == "__main__":
    root_json_dir = r"E:\BaiduNetdiskDownload\QD(1)\ann"
    root_save_xml_dir = r"E:\BaiduNetdiskDownload\QD(1)\xml_ann"
    for json_filename in tqdm(os.listdir(root_json_dir)):
        json_path = os.path.join(root_json_dir, json_filename)
        # print(json_path)
        save_xml_path = os.path.join(root_save_xml_dir, json_filename.replace(".json", ".xml"))
        json_transform_xml(json_path, save_xml_path)
