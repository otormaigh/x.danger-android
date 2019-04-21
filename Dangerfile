# Sometimes it's a README fix, or something like that - which isn't relevant for
# including in a project's CHANGELOG for example
declared_trivial = github.pr_title.include? "#trivial"

# Make it more obvious that a PR is a work in progress and shouldn't be merged yet
warn("PR is classed as Work in Progress") if github.pr_title.include? "[WIP]"

# Warn when there is a big PR
warn("Big PR") if git.lines_of_code > 500

# Android Lint
begin
  # Skip gradle lint task
  # It means we need to run lint tasks before running Danger
  android_lint.skip_gradle_task=true

  # Check modified/new files only
  android_lint.filtering=true

  # Default: Warning
  # android_lint.severity = "Error"

  # Report lint warnings
  Dir.glob("**/lint-results*.xml").each do |xml|
    android_lint.report_file=xml
    android_lint.lint(inline_mode: true)
  end
end

# LGTM
begin
  if status_report[:errors].length.zero? && status_report[:warnings].length.zero?
    markdown("Asserted successfully. :100:")
  end
end