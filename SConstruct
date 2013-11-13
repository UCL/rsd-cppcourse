import rsdpandoc.builders
import rsdpandoc.globbers
        
env=Environment(tools=['default',rsdpandoc.builders.add_builders])
#env["HavePIL"]=True
#env["HaveWSD"]=True
#env["HaveWebKit"]=True

sources = [
	Glob("introduction/*.md"),
	[Glob("session{session}/*.md".format(session=session)) for session in range(1,6)],
	Glob("appendices/*.md")
]

rsdpandoc.globbers.mixed_html_layout(sources,env)
#rsdpandoc.globbers.latex_layout(sources,env)