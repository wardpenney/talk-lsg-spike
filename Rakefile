desc "Start mdpress, which will watch `deck.md` and build your presentation automatically."
task :build do
  puts <<-'TEXT'
  ****************

  Starting a server to build your deck!

  1. Keep this terminal open, and
  2. `rake open` in a new terminal. Changes to `deck.md` will automatically be built, just
  3. refresh the page.

  Happy presentation-writing!

  ****************
  TEXT

  trap('INT') do
    puts "Exiting mdpress..."
    exit 0
  end

  sh "mdpress --automatic deck.md --stylesheet pivotal &"
end

desc "Open up your presentation."
task :open => :build do
  sh "launchy deck/index.html"
end

task :default => [:open]
