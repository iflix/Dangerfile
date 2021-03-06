#
# This Dangerfile is taken form https://github.com/iflix-letsplay/Dangerfile,
# feel free to open a pull request to suggest new rules or fixes.
#

# Make it more obvious that a PR is a work in progress and shouldn't be merged yet
warn('PR is classed as Work in Progress') if github.pr_title.include? '[WIP]'

# Warn when there is a big PR
warn('Big PR') if git.lines_of_code > 500

# Don't let testing shortcuts get into master by accident
fail('focused `describe` left in tests') if `grep -r fdescribe *Tests/ `.length > 1
fail('focused `it` left in tests') if `grep -r fit *Tests/ `.length > 1

# Make sure the commit message is formatted properly
# Rules: https://github.com/jonallured/danger-commit_lint#usage
commit_lint.check warn: :all

# Encourage writing up some reasoning about the PR, rather than just leaving a
# title
if github.pr_body.length < 5
  fail "Please provide a summary in the Pull Request description"
end

# Prevent merging PRs with commits intended to be rebased
if git.commits.any? { |c| c.message.include?('fixup!') || c.message.include?('squash!') }
  fail('This PR contains commits marked as squash or fixup. Please perform an interactive rebase to apply the changes.')
end
