
# -*- coding: utf-8 -*-
"""
Created on Fri Nov  6 09:06:59 2015

@author: dawenzi
"""

import requests
import os
quyu={'dongbei':'ANEC','huabei':'ANCN','huadong':'AECN','huazhong':'ACCN',\
      'huanan':'ASCN','xinan':'ASWC','xibei':'ANWC','changjiang':'ABCJ',\
       'huanghuai':'ABHH','dongnanyanhai':'ACES','quanguo':'ACHN'}
os.chdir('/home/dawenzi/python/')
#url='http://www.moc.cma.gov.cn/mocimg/radar/mosaic/AECN/QREF/2015/11/04/AECN.QREF000.20151104.010000.GIF'
nian=2015
for yue in range(11,12):
    for ri in range(5,6):
        ddate=str(nian)+str(yue).zfill(2)+str(ri).zfill(2)
        ll='/home/dawenzi/python/radar/'+ddate
        os.makedirs(ll)
        for hh in range(23,24):
            for mm in range(0,51,10):
                ttime=str(hh).zfill(2)+str(mm).zfill(2)
                url='http://www.moc.cma.gov.cn/mocimg/radar/mosaic/'+quyu['huadong']+'/QREF/'+str(nian)+'/'+str(yue).zfill(2)+'/'+str(ri).zfill(2)+'/'+quyu['huadong']+'.QREF000.'+ddate+'.'+ttime+'00.GIF'
                print(url)  
                os.chdir(ll)
                pic=requests.get(url)
                fp=open(ddate+ttime+'00'+'.gif','wb')
                fp.write(pic.content)
                fp.close()
