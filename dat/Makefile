.PHONY: dat/all dat/clean dat/distclean

dat/all: $(DAT_DATA_OBJECTS) $(DAT_ORACLES_OBJECTS) $(DAT_QUEST_OBJECTS) $(DAT_RUMORS_OBJECTS) $(DAT_DUNGEON_OBJECTS) $(DAT_SPEC_OBJECTS) $(DAT_QUEST_LEVEL_OBJECTS)

dat/clean:
	$(RM) $(DAT_DATA_OBJECTS) $(DAT_ORACLES_OBJECTS) $(DAT_QUEST_OBJECTS) $(DAT_RUMORS_OBJECTS) $(DAT_DUNGEON_OBJECTS) $(DAT_SPEC_OBJECTS) $(DAT_QUEST_LEVEL_OBJECTS) $(DAT_DUNGEON_GENERATED) $(CURDIR)/*.lev

dat/depclean:
	$(RM) $(CURDIR)/options.txt

$(DAT_DATA_OBJECTS): $(DAT_DATA_SOURCES) $(MAKEDEFS)
	$(MAKEDEFS) -d

$(DAT_ORACLES_OBJECTS): $(DAT_ORACLES_SOURCES) $(MAKEDEFS)
	$(MAKEDEFS) -h

# TODO: date.h should be rebuilt if _any_ source or header files change
# This is an ugly hack so I can add a proper multi-output target.
$(CURDIR)/options.% $(INCDIR)/date.%: $(MAKEDEFS)
	$(MAKEDEFS) -v

$(DAT_QUEST_OBJECTS): $(DAT_QUEST_SOURCES) $(MAKEDEFS)
	$(MAKEDEFS) -q

$(DAT_RUMORS_OBJECTS): $(DAT_RUMORS_SOURCES) $(MAKEDEFS)
	$(MAKEDEFS) -r

$(DAT_DUNGEON_GENERATED): $(DAT_DUNGEON_SOURCES) $(MAKEDEFS)
	$(MAKEDEFS) -e

$(DAT_DUNGEON_OBJECTS): %: %.pdf $(DGN_COMP)
	$(DGN_COMP) $<

# This uses touch which is an ugly hack. I hate it, and it should die.
$(DAT_SPEC_OBJECTS) $(DAT_QUEST_LEVEL_OBJECTS): %.lev: %.des $(LEV_COMP)
	$(LEV_COMP) $<
	$(TOUCH) $@
