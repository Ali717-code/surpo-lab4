# Лабораторная работа 4. Перебазирование

## До rebase

### $ git log --oneline --graph --all
* 4429059 master: m.txt
* eba22f1 master: b=MASTER
| * 49d0e7b topic: b=TOPIC
| * e8fd9c9 topic: t.txt
|/  
* dc01199 initial

### $ git rebase master
Rebasing (1/2)Rebasing (2/2)Auto-merging f.txt
CONFLICT (content): Merge conflict in f.txt
error: could not apply 49d0e7b... topic: b=TOPIC
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
hint: Disable this message with "git config set advice.mergeConflict false"
Could not apply 49d0e7b... # topic: b=TOPIC

### $ git status --short
UU f.txt
[detached HEAD 0e5b172] topic: b=TOPIC
 1 file changed, 1 insertion(+), 1 deletion(-)
Successfully rebased and updated refs/heads/topic.

## После rebase (линейная история)

### $ git log --oneline --graph --all
* 0e5b172 topic: b=TOPIC
* b7fcf7f topic: t.txt
* 4429059 master: m.txt
* eba22f1 master: b=MASTER
* dc01199 initial

### $ git merge --ff-only topic
Updating 4429059..0e5b172
Fast-forward
 f.txt | 2 +-
 t.txt | 1 +
 2 files changed, 2 insertions(+), 1 deletion(-)
 create mode 100644 t.txt

### $ git log --oneline --graph
* 0e5b172 topic: b=TOPIC
* b7fcf7f topic: t.txt
* 4429059 master: m.txt
* eba22f1 master: b=MASTER
* dc01199 initial

## Merge vs Rebase
- merge сохраняет реальную историю и создаёт merge-коммит; безопасен для общих веток.
- rebase переписывает коммиты и делает историю линейной; применять только к локальным/неопубликованным веткам.
