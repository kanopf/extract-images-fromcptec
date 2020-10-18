# extract-images-fromcptec
Code for extract images from GOES SAT on site of Cptec/INPE with python.


def dl_jpg(url, file_path, file_name):
    try:
        full_path = file_path + file_name + '.jpg'
        urllib.request.urlretrieve(url, full_path)
        
    except:
        pass
    
banda = 'goes 16 3.90 micro'
ano = 2019
mes = 7
diai= 1 #sempre um dia antes para bater com contador diai = diai+1
diaf = 31
hora = 0 #cuidado com este trexo devido a algumas bandas começarem em outros horarios, este caso funciona para hora <100

for dia in range (diai, diaf+1,1):
    for hora in range (hora, 2400, 10):
        
        if hora < 2300 :
            U = (('{:04d}{:02d}{:02d}{:04d}').format(ano,mes,dia,hora))
            url ="http://satelite.cptec.inpe.br/repositoriogoes/goes16/goes16_web/ams_ret_ch07_baixa/2019/07/S11635376_{0}.jpg".format(U)
            file_name = (U)
            dl_jpg(url, '/home/qiep/Área de Trabalho/kanopf/2019/imagens/IMAGENSGOES16 3.90 MICRO/{0}'.format(banda), file_name)
        elif hora == 2300:
            break
    hora = 0