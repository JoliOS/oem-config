all: update

templates.pot: ../oem-config.templates-imported
	debconf-updatepo --skip-merge --podir=.

update: templates.pot
	@if [ -z "$(GTK_PO)" ]; then \
		echo "Set GTK_PO to the location of a current GTK+ po/ directory." >&2; \
		exit 1; \
	fi
	rm -f *.po
	for p in $(GTK_PO)/*.po; do \
		[ -f "$$p" ] || continue; \
		b="$$(basename "$$p")"; \
		[ -f "../po/$$b" ] || continue; \
		msgmerge -q "$$p" templates.pot | \
		msgattrib --translated --no-fuzzy --no-obsolete -o "$$b" -; \
	done
