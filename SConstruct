import rsdpandoc.builders
import rsdpandoc.globbers
        
env=Environment(tools=['default',rsdpandoc.builders.add_builders])
#env["HavePIL"]=True
#env["HaveWSD"]=True
#env["HaveWebKit"]=True

intro=Glob("introduction/*.md")
sessions={}
for session in range(1,6):
	sessions["session{session}".format(session=session)]=Glob("session{session}/*.md".format(session=session))
appendices=Glob("appendices/*.md")
sessions["intro"]=intro
sessions["appendices"]=appendices
session_names=["intro", "session1", "session2","session3","session4","session5","appendices"]

sources=[sessions[name] for name in session_names]

rsdpandoc.globbers.reveal_layout(sources,env)
#rsdpandoc.globbers.latex_layout(sources,env)