# URLXMLTOTXT
import urllib
import os
#import argparse
import sys
from xml.etree.ElementTree import ElementTree
#import csv



route = urllib.urlopen('http://tracking.marka-usa.com/radiomar/')
contents  =  route.read()
route.close()
print contents

def Readthexml(f):
	contents = ElementTree()
	contents.parse(f)
	doc = [contents.find('mobile').text, contents.find('date').text, 
	       contents.find('lat'), contents.find('long'), contents.find('velocity'), 
	       contents.find('id')]
	out = open(f + '.txt', 'w')
	out.write('\n\n'.join(doc))
	return True

def main(argv=None):
    if argv is None:
        argv = sys.argv
        args = argv[1:]
        for arg in args:
            if os.path.exists(arg):
                Readthexml(arg)

if __name__ == "__main__":
    main()
