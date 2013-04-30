# Front End Testing for Skeptics

Luke Francl, Swiftype

## Third Party Javascripts

Get the Third-Party Javascript book by Vinegar and Kovalyov.

## Tools

1. Capybara
2. PhantomJS - headless webkit browser
3. Poltergeist - Ruby code for Capybara::PhantomJS

## PhantomJS

`brew install phantomjs`

Add Capybara and Poltergeist to your Gemfile

Set `Capybara.javascript_drive = :poltergeist`

http://github.com/loog/frontend-testing-for-skeptics

### Debugging

`page.driver.debug`

Make use of `evaluate_script` feature. You can run javascript commands with the DOM context!

## modeset/teabag gem

`gem install teabag`

## Perceptual Diffs

Check differences in what you see.