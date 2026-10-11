source "https://rubygems.org"

# Pinned to the Jekyll stack GitHub Pages runs natively (no Actions workflow).
gem "github-pages", "232", group: :jekyll_plugins

# Ruby 3 removed webrick from the standard library. Needed for local `jekyll serve`.
# Omitted when GitHub builds the site, so the Pages gem set stays satisfied.
install_if -> { ENV["GITHUB_ACTIONS"] != "true" } do
  gem "webrick", "~> 1.8"
end
