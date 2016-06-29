TURBO_SIM=$(shell python -c "import os,Cattery.Siamese ; print \"%s/turbo-sim.py\" % Cattery.Siamese.__path__[0]")
.PHONY: all clean_tmps clean pols clean_mfs mfs
all: pols mfs
clean_tmps:
	rm -f *.obj *.DicoFacet *.reg *.log
clean_pols: clean_tmps
	rm -rf polarized_sky.MS_p0
pols: clean_pols
	makems pols.makems.parset
	meqtree-pipeliner.py -c polarized_sky.tdl --mt=4 @pol $(TURBO_SIM) =simulate
clean_mfs: clean_tmps
	rm -rf mfs_sky.MS_p0
mfs: clean_mfs
	makems mfs.makems.parset
	meqtree-pipeliner.py -c mfs_sky.tdl --mt=4 @mfs $(TURBO_SIM) =simulate
clean: clean_pols clean_mfs
