
# Per https://docs.pagure.org/copr.copr/user_documentation.html#make-srpm
# the make is invoked as
# make -f <cloned_repodir>/.copr/Makefile srpm outdir="<outdir>" spec="<spec_path>"

spec_dir = $(dir $(spec))

srpm:
	spectool --version || dnf install -y /usr/bin/spectool
	cd $(spec_dir) && spectool -g $(spec)
	cd $(spec_dir) && rpmbuild -D '_srcrpmdir $(outdir)' -D '_sourcedir .' -bs $(spec)

