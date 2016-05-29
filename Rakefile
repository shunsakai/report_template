task :default => ["build", 'clean']

name = "thesis"

desc "Convert markdown file into tex"
task :build do
  Dir.glob("src/*.md").map { |md|
    tex = md.sub(".md", ".tex")
    `pandoc #{md} -o #{tex}`
  }
  puts `platex -kanji=UTF8 #{name}.tex`
  puts `dvipdfmx #{name}.dvi`
  puts `mv #{name}.pdf build/`
end

task :clean do
  Dir.glob("src/*.md").map { |md|
    tex = md.sub(".md", ".tex")
    if md != 'src/thesis.tex'
      `rm #{tex}`
    end
  }

  `rm *.log`
  `rm *.aux`
  `rm src/*.aux`
  `rm *.dvi`
  `rm *.lof`
  `rm *.toc`
  `rm *.lot`
end

task :open do
  `open build/thesis.pdf`
end


task :abstract => ["build_abstract", 'clean']
task :build_abstract do
  puts `platex src/abstract.tex`
  puts `dvipdfmx abstract.dvi`
  puts `mv abstract.pdf build/`
end
task :open_abstract do
  `open build/abstract.pdf`
end

task :eps do
  Dir.glob('src/images/**/*.png').each {|png|
    eps = png.sub(".png", ".eps")
    p `convert #{png} #{eps}`
  }
end

#
# convert SHIFT_JIS into UTF-8
# iconv -s -f SHIFT_JIS -t UTF-8 hoge.sty > hoge.utf8.sty
# sed -e 's/¥/\\/g' -e 's/‾/~/g' paper_utf8.tex > paper_out.tex
#
# #!/bin/bash

# Default file name
# filename="paper"

# Get file name from parameter
# if [ $1 ]; then
#    filename=$1
#fi
#
# Make .dvi and .pdf file
#
# platex $filename.tex
# pbibtex $filename.aux
# platex $filename.tex
# dvipdfmx -p a4 $filename.dvi
#
# preview
# open $filename.pdf
