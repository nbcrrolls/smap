# $Id: Makefile,v 1.5 2012/10/09 17:28:47 clem Exp $
#
# @Copyright@
# 
# 				Rocks(r)
# 		         www.rocksclusters.org
# 		         version 5.5 (Mamba)
# 		         version 6.0 (Mamba)
# 
# Copyright (c) 2000 - 2012 The Regents of the University of California.
# All rights reserved.	
# 
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are
# met:
# 
# 1. Redistributions of source code must retain the above copyright
# notice, this list of conditions and the following disclaimer.
# 
# 2. Redistributions in binary form must reproduce the above copyright
# notice unmodified and in its entirety, this list of conditions and the
# following disclaimer in the documentation and/or other materials provided 
# with the distribution.
# 
# 3. All advertising and press materials, printed or electronic, mentioning
# features or use of this software must display the following acknowledgement: 
# 
# 	"This product includes software developed by the Rocks(r)
# 	Cluster Group at the San Diego Supercomputer Center at the
# 	University of California, San Diego and its contributors."
# 
# 4. Except as permitted for the purposes of acknowledgment in paragraph 3,
# neither the name or logo of this software nor the names of its
# authors may be used to endorse or promote products derived from this
# software without specific prior written permission.  The name of the
# software includes the following terms, and any derivatives thereof:
# "Rocks", "Rocks Clusters", and "Avalanche Installer".  For licensing of 
# the associated name, interested parties should contact Technology 
# Transfer & Intellectual Property Services, University of California, 
# San Diego, 9500 Gilman Drive, Mail Code 0910, La Jolla, CA 92093-0910, 
# Ph: (858) 534-5815, FAX: (858) 534-7345, E-MAIL:invent@ucsd.edu
# 
# THIS SOFTWARE IS PROVIDED BY THE REGENTS AND CONTRIBUTORS ``AS IS''
# AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
# THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
# PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE REGENTS OR CONTRIBUTORS
# BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
# CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
# SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR
# BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
# WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE
# OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN
# IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
# 
# @Copyright@
#
# $Log: Makefile,v $
# Revision 1.5  2012/10/09 17:28:47  clem
# removed urgent queue from opal script
# create log directory in the job WD
#
# Revision 1.4  2012/08/29 22:12:16  clem
# As ugly as it can get!!
#
# Obviously spooling of temporary txt file is done in the same directory
# where the binaries are!
# So we have a directory where the binaries are which must be writable by users :-(
#
# The spooling path is hardcoded in the java class
#
# Revision 1.3  2012/08/28 21:00:37  clem
# Second round of fixes
#
#  - added jmol
#  - fixes several path problem in the script
#  - created a shared area for creating temporary files
#  - removed some useless log file from the smap.tar.gz
#
# Revision 1.2  2012/08/28 05:16:29  clem
# first round of fixes
#
# Revision 1.1  2012/08/27 19:18:14  clem
# First attempt with smap. All this is a big hack, I could not get the source code
# so I copyed file from kriptonite and using sed to fix path problem.
#
# Revision 1.1  2012/06/20 00:22:15  clem
# first version of the browndye roll
#

REDHAT.ROOT = $(CURDIR)/../../

-include $(ROCKSROOT)/etc/Rules.mk
include Rules.mk


build:
	gunzip -c $(NAME).$(TARBALL_POSTFIX) | $(TAR) -xf -
	( 							\
		cd $(NAME);				\
		for i in `grep -rl /nas/opaluser/smap *`;do \
			sed -i 's:/nas/opaluser/smap:/opt/smap:g' $$i ;\
		done \
	)
	patch -p0 < patch
	# remove urgent queue requeste in qsub script
	patch -p0 < patch_urgent
	rm -rf smap/LOCAL_PDB_DIR/PDB
	ln -s /share/opal/smap/PDB smap/LOCAL_PDB_DIR/PDB
	# as ugly as it can get 
	# obviously spooling of temporary txt file is done in the same directory 
	# where the binaries are! so it need to be writable by users :-(
	chmod 777 smap/external/qhull/linux/
	
install::
	mkdir -p $(ROOT)/$(PKGROOT)
	(							\
		cp -a $(NAME)/* $(ROOT)/$(PKGROOT);		\
	)

clean::
	rm -rf $(NAME)-$(VERSION)
