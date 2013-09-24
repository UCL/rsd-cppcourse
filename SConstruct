import os

pandoc_latex=Builder(action='pandoc --template=report -V documentclass=scrartcl -V'+
	' links-as-notes -V linkcolor="uclmidgreen" --number-sections $SOURCES -o $TARGET')

env=Environment()
env.Append(BUILDERS={'PandocLatex':pandoc_latex})
intro=Glob("introduction/*.md")
sessions={"session{session}".format(session=session):Glob("session{session}/*.md".format(session=session)) 
	for session in range(1,4)}
appendices=Glob("appendices/*.md")
sessions["intro"]=intro
sessions["appendices"]=appendices
session_names=["intro", "session1", "session2","appendices"]
notes=env.PandocLatex('CPP.pdf',[sessions[name] for name in session_names])
Depends(notes,'report.latex')

pandoc_slides=Builder(action='pandoc -t revealjs -s -V theme=beige'+
	' --css=beige.css'+
	' --css=slidetheme.css'+
	' -V revealjs-url=http://lab.hakim.se/reveal-js/'+
	' $SOURCES -o $TARGET')
env.Append(BUILDERS={'PandocSlides':pandoc_slides})
slides=env.PandocSlides("reveal/index.html",[sessions[name] for name in session_names])
