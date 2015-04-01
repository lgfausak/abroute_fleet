#
# Makefile to produce a write_files.cloud segment
# this file can be prepended to the cloud config file
# for pre installed service files on the fleet nodes
#
.SUFFIXES: .service .cloud

S=\
  abdata.cloud\
  pg.cloud\
  router.cloud\
  rpc.cloud

D=/etc/systemd/system/
O=core
G=core
T=/tmp/t.$$

.service.cloud:
	@echo 'building .cloud file '$@
	@echo 'write_files:' > $T
	@echo '  - path: '$D$< >> $T
	@echo '    permissions: 0644' >> $T
	@echo '    owner: '$O:$G >> $T
	@echo '    encoding: gzip+base64' >> $T
	@echo '    content: |' >> $T
	@gzip < $< | base64 | sed 's/^/      /' >> $T
	@mv $T $@

all.cloud: write_files.cloud build.cloud
	touch all.cloud
	echo all done.

write_files.cloud: $S
	cat $S > $@
	echo 'everything done...'

build.cloud: $A
	cat $A > $@
	echo 'build done...'

clean:
	rm -f $S write_files.cloud build.cloud all.cloud
