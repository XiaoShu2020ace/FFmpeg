APITESTPROGS-$(call ENCDEC, FLAC, FLAC) += api-flac
APITESTPROGS-$(call DEMDEC, H264, H264) += api-h264
APITESTPROGS-$(call DEMDEC, H264, H264) += api-h264-slice
APITESTPROGS-yes += api-seek api-dump-stream-meta
APITESTPROGS-$(call DEMDEC, H263, H263) += api-band
APITESTPROGS-$(HAVE_THREADS) += api-threadmessage
APITESTPROGS += $(APITESTPROGS-yes)

APITESTOBJS  := $(APITESTOBJS:%=$(APITESTSDIR)%) $(APITESTPROGS:%=$(APITESTSDIR)/%-test.o)
APITESTPROGS := $(APITESTPROGS:%=$(APITESTSDIR)/%-test$(EXESUF))
-include $(wildcard $(APITESTOBJS:.o=.d))

$(APITESTOBJS): | $(sort $(dir $(APITESTOBJS)))
$(APITESTOBJS) $(APITESTOBJS:.o=.i): CPPFLAGS += -DTEST
$(APITESTOBJS) $(APITESTOBJS:.o=.i): CFLAGS += -Umain

$(APITESTPROGS): %$(EXESUF): %.o $(FF_DEP_LIBS)
	$(LD) $(LDFLAGS) $(LDEXEFLAGS) $(LD_O) $(filter %.o,$^) $(FF_EXTRALIBS) $(ELIBS)

testclean::
	$(RM) $(addprefix $(APITESTSDIR)/,$(CLEANSUFFIXES) *-test$(EXESUF))
