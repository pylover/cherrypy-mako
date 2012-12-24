.. pymlconf documentation master file, created by
   Vahid Mardani on Sat Apr 14 05:05:05 2012.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Cherrypy's Mako Plugin
====================================

``CherrypyMako`` is a cherrypy plugin that provides Mako template engine , within cherrypy as a tool.

Example:

demo.py::

	import os.path
	import cherrypy
	import CherrypyMako
	import datetime
	CherrypyMako.setup()
	root_dir = os.path.abspath( os.path.dirname(__file__))
	 
	class Root(object):
	    
	    @cherrypy.expose
	    @cherrypy.tools.mako(filename='index.html')
	    def index(self):
	        return {'currentTime':datetime.datetime.now()}
	
	    
	_cp_config={
	    'global':{
	        'server.socket_host'  : '0.0.0.0', 
	        'server.socket_port'  : 1919,
	        'tools.mako.directories' : [os.path.join(root_dir,'templates')],
	    },
	}
	
	if __name__ == '__main__':
	    cherrypy.quickstart(Root(), '', config=_cp_config)

index.html::

	<html>
		<head>
			<title>Cherrypy Mako Tool Demo</title>
		</head>
		<body>
			${currentTime}
		</body>
	</html>