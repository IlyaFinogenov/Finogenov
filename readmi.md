Упорядочивание коммитов
Вы также можете использовать интерактивное перебазирование для изменения порядка или полного
удаления коммитов. Если вы хотите удалить коммит «Add cat-file» и изменить порядок, в котором
были внесены два оставшихся, то вы можете изменить скрипт перебазирования с такого:
pick f7f3f6d Change my name a bit
pick 310154e Update README formatting and add blame
pick a5f4a0d Add cat-file
на такой:
pick 310154e Update README formatting and add blame
pick f7f3f6d Change my name a bit
Когда вы сохраните скрипт и выйдете из редактора, Git переместит вашу ветку на родителя этих
коммитов, применит 310154e, затем f7f3f6d и после этого остановится. Вы, фактически, изменили
порядок этих коммитов и полностью удалили коммит «Add cat-file».
Объединение коммитов
С помощью интерактивного режима команды rebase также можно объединить несколько коммитов в
один. Git добавляет полезные инструкции в сообщение скрипта перебазирования:
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# . create a merge commit using the original merge commit's
# . message (or the oneline, if no original merge commit was
# . specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
Если вместо «pick» или «edit» вы укажете «squash», Git применит изменения из текущего и
предыдущего коммитов и предложит вам объединить их сообщения. Таким образом, если вы хотите
из этих трёх коммитов сделать один, вы должны изменить скрипт следующим образом:
pick f7f3f6d Change my name a bit
squash 310154e Update README formatting and add blame
squash a5f4a0d Add cat-file
Когда вы сохраните скрипт и выйдете из редактора, Git применит изменения всех трёх коммитов и
затем вернёт вас обратно в редактор, чтобы вы могли объединить сообщения коммитов:
# This is a combination of 3 commits.
# The first commit's message is:
Change my name a bit
# This is the 2nd commit message:
Update README formatting and add blame
# This is the 3rd commit message:
Add cat-file
После сохранения сообщения, вы получите один коммит, содержащий изменения всех трёх коммитов,
существовавших ранее.
