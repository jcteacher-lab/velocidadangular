# ============================================================
#  Makefile — Compilación de la guía "Velocidad Angular"
#  Autor: MTI. Juan Carlos Santiago Sánchez
#  Licencia: GNU GPL v3
# ============================================================

# ---------- Variables ----------
TEX       = pdflatex
BIB       = bibtex
MAIN      = VelocidadAngular
GUIDE_DIR = docs/guia-ejercicios
AUX_EXTS  = aux log out toc lof lot nav snm vrb fls fdb_latexmk synctex.gz
PDF_EXTS  = pdf

# ---------- Reglas principales ----------

.PHONY: all guia bib clean distclean help serve

## Compila todo (guía principal)
all: guia

## Compila la guía de ejercicios (dos pasadas para referencias)
guia:
	@echo "🔨 Compilando $(MAIN).tex (pasada 1)..."
	$(TEX) -interaction=nonstopmode $(MAIN).tex
	@echo "🔨 Compilando $(MAIN).tex (pasada 2)..."
	$(TEX) -interaction=nonstopmode $(MAIN).tex
	@echo "✅ PDF generado: $(MAIN).pdf"

## Compila la guía con referencias bibliográficas (BibTeX)
bib:
	@echo "🔨 Compilando $(MAIN).tex (pasada 1)..."
	$(TEX) -interaction=nonstopmode $(MAIN).tex
	@echo "📚 Ejecutando BibTeX..."
	-$(BIB) $(MAIN)
	@echo "🔨 Compilando $(MAIN).tex (pasada 2)..."
	$(TEX) -interaction=nonstopmode $(MAIN).tex
	@echo "🔨 Compilando $(MAIN).tex (pasada 3)..."
	$(TEX) -interaction=nonstopmode $(MAIN).tex
	@echo "✅ PDF generado con bibliografía: $(MAIN).pdf"

## Compila la guía dentro de docs/guia-ejercicios/ (si se mueve el .tex)
guia-docs:
	@echo "🔨 Compilando guía en $(GUIDE_DIR)/..."
	cd $(GUIDE_DIR) && $(TEX) -interaction=nonstopmode guia-ejercicios.tex
	cd $(GUIDE_DIR) && $(TEX) -interaction=nonstopmode guia-ejercicios.tex
	@echo "✅ PDF generado: $(GUIDE_DIR)/guia-ejercicios.pdf"

## Limpia archivos auxiliares
clean:
	@echo "🧹 Limpiando archivos auxiliares..."
	@for ext in $(AUX_EXTS); do \
		rm -f *.$$ext $(GUIDE_DIR)/*.$$ext 2>/dev/null; \
	done
	@echo "✅ Limpieza completada."

## Limpia archivos auxiliares Y el PDF generado
distclean: clean
	@echo "🗑️  Eliminando PDFs generados..."
	@for ext in $(PDF_EXTS); do \
		rm -f *.$$ext $(GUIDE_DIR)/*.$$ext 2>/dev/null; \
	done
	@echo "✅ Limpieza profunda completada."

## Sirve el simulador localmente (si existe index.html)
serve:
	@echo "🌐 Sirviendo en http://localhost:8000"
	python3 -m http.server 8000

## Ayuda
help:
	@echo "=================================================="
	@echo "  Makefile — Guía de Velocidad Angular"
	@echo "=================================================="
	@echo "Uso:  make [objetivo]"
	@echo ""
	@echo "Objetivos disponibles:"
	@echo "  make           → Compila la guía (2 pasadas)"
	@echo "  make guia      → Igual que 'make'"
	@echo "  make bib       → Compila con BibTeX (3 pasadas)"
	@echo "  make guia-docs → Compila la guía en docs/guia-ejercicios/"
	@echo "  make clean     → Borra archivos auxiliares"
	@echo "  make distclean → Borra auxiliares + PDF"
	@echo "  make serve     → Sirve el simulador en localhost:8000"
	@echo "  make help      → Muestra esta ayuda"
	@echo "=================================================="

# ---------- Regla por defecto ----------
.DEFAULT_GOAL := guia