all: index.html index-cn.html

index.html: blog.html
	mv blog.html index.html

index-cn.html: blog_cn.html
	mv blog_cn.html index-cn.html
	
../blog.tar.bz2: blog.pdf blog.html
	cd ..; tar cvfj blog.tar.bz2 blog

%.md: %.pptx
	pptx2md $< -o $@
	sed -i -e 's/<img src="\(.*\)".*\/>/![](\1)\\/g' $@

%.pdf: %.md
	pandoc $< -o $@ --latex-engine=xelatex --data-dir=. -H make-font-footnotesize.tex --highlight-style=espresso

%.html: %.md
	pandoc $< -o $@ -c github-pandoc.css -s --toc --highlight-style pygments
