# Info: only sections 1 and 7 are allowed.
# This is done by checking the section of the manual in install
# and by only making the man1 and man7 dirs when initialising
# a manual location in $(DEST).
SHELL:=/bin/bash
# DEST=/usr/share/man
DEST=$(HOME)/.local/man
MANUAL_PATTERN=\w+?\.([17])$

.PHONY: all install uninstall

all: install

install: $(DEST)
	@for f in *; do \
		if [[ "$$f" =~ $(MANUAL_PATTERN) ]] ; then \
			dest_file=$(DEST)/man$${BASH_REMATCH[1]}/"$$f" ;\
			cp "$$f" "$${dest_file}" ;\
			gzip "$${dest_file}" ;\
		fi ;\
	done

uninstall:
	@for f in *; do \
		if [[ "$$f" =~ $(MANUAL_PATTERN) ]] ; then \
			section=$${BASH_REMATCH[1]} ;\
			rm "$(DEST)"/man$${section}/"$$f".gz ;\
		fi ;\
	done

$(DEST):
	@read -p 'About to mkdir $(DEST). Confirm? (y/N): ' ans && \
		case "$$ans" in \
			y) mkdir -p "$(DEST)"/{man1,man7} ;; \
			*) echo Not making $(DEST) ;; \
		esac
