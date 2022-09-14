# Git Style Guide
# Git-ის სტილისტიკის სახელმძღვანელო

Translations are available in the following languages:
წინამდებარე სახელმძღვანელოს თარგმანები ხელმისაწვდომია შემდეგ ენებზე:

* [Chinese (Simplified)](https://github.com/aseaday/git-style-guide)
* [Chinese (Traditional)](https://github.com/JuanitoFatas/git-style-guide)
* [English](https://github.com/agis/git-style-guide)
* [French](https://github.com/pierreroth64/git-style-guide)
* [German](https://github.com/runjak/git-style-guide)
* [Greek](https://github.com/grigoria/git-style-guide)
* [Italian](https://github.com/vincendep/git-style-guide)
* [Japanese](https://github.com/objectx/git-style-guide)
* [Korean](https://github.com/ikaruce/git-style-guide)
* [Polish](https://github.com/mbiesiad/git-style-guide/tree/pl_PL)
* [Portuguese](https://github.com/guylhermetabosa/git-style-guide)
* [Russian](https://github.com/alik0211/git-style-guide)
* [Spanish](https://github.com/jeko2000/git-style-guide)
* [Thai](https://github.com/zondezatera/git-style-guide)
* [Turkish](https://github.com/CnytSntrk/git-style-guide)
* [Ukrainian](https://github.com/denysdovhan/git-style-guide)

# Table of contents
# სარჩევი

- [Git Style Guide](#git-style-guide)
- [Git-ის სტილისტიკის სახელმძღვანელო](#git-ის-სტილისტიკის-სახელმძღვანელო)
- [Table of contents](#table-of-contents)
- [სარჩევი](#სარჩევი)
  - [Branches](#branches)
  - [განშტოებები (Branches)](#განშტოებები-branches)
  - [Commits](#commits)
  - [Commit-ები](#commit-ები)
    - [Messages](#messages)
    - [შეტყობინებები](#შეტყობინებები)
  - [Merging](#merging)
  - [Misc.](#misc)
- [License](#license)
- [Credits](#credits)

## Branches
## განშტოებები (Branches)

* Choose *short* and *descriptive* names:
* შეარჩიეთ *მოკლე* და *აღწერითი* სახელები:

  ```shell
  # good # კარგია
  $ git checkout -b oauth-migration

  # bad - too vague # ცუდია - ძალიან ბუნდოვანია
  $ git checkout -b login_fix
  ```

* Identifiers from corresponding tickets in an external service (eg. a GitHub
  issue) are also good candidates for use in branch names. For example:
* იდენტიფიკატორები შესაბამისი გარე სერვისებიდან (მაგ. Github issue),
  ასევე მშვენიერი კანდიტატები არიან განშტოების სახელებში გამოსაყენებლად. მაგალითად:

  ```shell
  # GitHub issue #15
  $ git checkout -b issue-15
  ```

* Use lowercase in branch names. External ticket identifiers with uppercase
  letters are a valid exception. Use *hyphens* to separate words.
* განშტოების სახელთა ჩაწერისათვის გამოიყენეთ პატარა ასოები. გარე სერვისთა იდენტიფიკატორების დიდი ასოებით ჩაწერა დასაშვები გამონაკლისია.
  სიტყვების ერთმანეთისგან გამოსაყოფად გამოიყენეთ ტირეები.

  ```shell
  $ git checkout -b new-feature      # good # კარგია
  $ git checkout -b T321-new-feature # good (Phabricator task id) # კარგია (Phabricator task id)
  $ git checkout -b New_Feature      # bad # ცუდია
  ```

* When several people are working on the *same* feature, it might be convenient
  to have *personal* feature branches and a *team-wide* feature branch.
  Use the following naming convention:
* როდესაც *ერთ* ფუნქციონალზე რამდენიმე ადამიანი მუშაობს, შესაძლოა მოსახერხებელი იყოს,
  თუკი თითოეულს გამოუყოფთ *პირად* განშტოებას და ცალკე გექნებათ *მთელი გუნდისათვის საერთო* განშტოება.
  გამოიყენეთ შემდეგი სახელდების კანონზომიერება:

  ```shell
  $ git checkout -b feature-a/main # team-wide branch # მთელი გუნდისათვის საერთო განშტოება
  $ git checkout -b feature-a/maria  # Maria's personal branch # მარიას პირადი განშტოება
  $ git checkout -b feature-a/nick   # Nick's personal branch # ნიკის პირადი განშტოება
  ```

  Merge at will the personal branches to the team-wide branch (see ["Merging"](#merging)).
  Eventually, the team-wide branch will be merged to "main".
  სურვილისამებრ მოახდინეთ პირადი განშტოებების შერწყმა მთელი გუნდისათვის საერთო განშტოებასთან (იხ. [„შერწყმა“](#merging)).
  საბოლოოდ, მთელი გუნდისათვის საერთო განშტოება შეერწყმება მთავარ („main“) განშტოებას.

* Delete your branch from the upstream repository after it's merged, unless
  there is a specific reason not to.

  Tip: Use the following command while being on "main", to list merged
  branches:
* შერწყმის შემდეგ წაშალეთ განშტოება,
  თუკი აღარ აპირებთ მის გამოყენებას.

  რჩევა: მთავარ („main“) განშტოებაზე ყოფნისას გაუშვით შემდეგი ბრძანება, რათა ნახოთ შერწყმული
  განშტოებები:

  ```shell
  $ git branch --merged | grep -v "\*"
  ```

## Commits
## Commit-ები

* Each commit should be a single *logical change*. Don't make several
  *logical changes* in one commit. For example, if a patch fixes a bug and
  optimizes the performance of a feature, split it into two separate commits.

  *Tip: Use `git add -p` to interactively stage specific portions of the
  modified files.*
* თითოეული commit-ი უნდა წარმოადგენდეს ერთ *ლოგიკურ ცვლილებას*. ნუ გააერთიანებთ რამდენიმე *ლოგიკურ ცვლილებას* ერთ commit-ში.
  მაგალითად, თუ გამოასწორეთ ხარვეზი და გააუმჯობესეთ წარმადობა,
  უმჯობესია ცვლილებები დაყოთ ორ დამოუკიდებელ commit-ად.

  *რჩევა: გამოიყენეთ `git add -p` [ბრძანება] მოდიფიცირებულ ფაილთა ცალკეული ნაწილების
  ინტერაქტიულად ორგანიზებისათვის.*

* Don't split a single *logical change* into several commits. For example,
  the implementation of a feature and the corresponding tests should be in the
  same commit.
* არ დაყოთ ერთი *ლოგიკური ცვლილება* რამდენიმე commit-ად. მაგალითად,
  ფუნქციონალის რეალიზაცია და [მისთვის] სათანადო ტესტები უნდა გაერთიანდეს ერთსა და იმავე
  commit-ში.

* Commit *early* and *often*. Small, self-contained commits are easier to
  understand and revert when something goes wrong.
* განახორციელეთ commit-ები *დროულად* და *ხშირად*. მოკლე, თვითმყოფადი commit-ები მეტად მარტივად გასაგებია და
  ამარტივებს უწინდელ მდგომარეობაში დაბრუნებას, თუკი რაიმე არასწორად მოხდება.

* Commits should be ordered *logically*. For example, if *commit X* depends
  on changes done in *commit Y*, then *commit Y* should come before *commit X*.
* commit-ები *ლოგიკური* თანმიმდევრობით უნდა განხორციელდეს. მაგალითად, თუ *commit X* დამოკიდებულია
  *commit Y*-ში შესრულებულ ცვლილებებზე, მაშინ *commit Y* უნდა განხორციელდეს *commit X*-ამდე.

Note: While working alone on a local branch that *has not yet been pushed*, it's
fine to use commits as temporary snapshots of your work. However, it still
holds true that you should apply all of the above *before* pushing it.
შენიშვნა: ვიდრე მარტო მუშაობთ ადგილობრივ (*ლოკალურ*) განშტოებაზე, რომლის *ატვირთვაც (push) ჯერ არ მომხდარა*,
დასაშვებია commit-ების, როგორც თქვენი სამუშაოს დროებითი ჩანაწერების, გამოყენება. თუმცა,
ისევ და ისევ მართებულია ზემოთ მოყვანილი რეკომენდაციების დაცვა, *ვიდრე* ატვირთვას განახორციელებდეთ.

### Messages
### შეტყობინებები

* Use the editor, not the terminal, when writing a commit message:
* როდესაც წერთ commit-ის აღწერას, ბრძანებათა სტრიქონის (*ტერმინალის*) ნაცვლად გამოიყენეთ რედაქტორი:

  ```shell
  # good # კარგია
  $ git commit

  # bad # ცუდია
  $ git commit -m "Quick fix"
  ```

  Committing from the terminal encourages a mindset of having to fit everything
  in a single line which usually results in non-informative, ambiguous commit
  messages.
  ბრძანებათა სტრიქონის (*ტერმინალის*) გამოყენება commit-ისთვის გზღუდავთ - გიწევთ ყველაფრის ერთ ხაზში ჩატევა,
  რაც, ჩვეულებრივ, შეტყობინებებს არაინფორმაციულსა და
  ბუნდოვანს ხდის.

* The summary line (ie. the first line of the message) should be
  *descriptive* yet *succinct*. Ideally, it should be no longer than
  *50 characters*. It should be capitalized and written in imperative present
  tense. It should not end with a period since it is effectively the commit
  *title*:
* სათაური (ანუ შეტყობინების პირველი ხაზი) უნდა იყოს
  *აღწერითი*, მაგრამ *ლაკონიური*. იდეალურ შემთხვევაში იგი უნდა შედგებოდეს
  არაუმეტეს *50 სიმბოლოსაგან*. ჩანაწერი უნდა იწყებოდეს დიდი ასოთი და დაიწეროს იმპერატიულ (*ბრძანებით*) აწმყო დროში.
  ბოლოში წერტილს ნუ დასვამთ, რადგან, ფაქტობრივად *სათაურს* წერთ:

  ```shell
  # good - imperative present tense, capitalized, fewer than 50 characters # კარგია - ბრძანებითი აწმყო დროშია, დიდი ასოთი იწყება, შედგება 50-ზე ნაკლები სიმბოლოსაგან
  Mark huge records as obsolete when clearing hinting faults

  # bad # ცუდია
  fixed ActiveModel::Errors deprecation messages failing when AR was used outside of Rails.
  ```

* After that should come a blank line followed by a more thorough
  description. It should be wrapped to *72 characters* and explain *why*
  the change is needed, *how* it addresses the issue and what *side-effects*
  it might have.
* ამის შემდეგ უნდა მოდიოდეს ცარიელი სტრიქონი, რომელსაც მოსდევს უფრო საგულდაგულო აღწერა.
  აღწერა უნდა შედგებოდეს მაქსიმუმ *72 სიმბოლოსაგან* და უნდა განმარტავდეს,
  თუ *რატომ* იყო საჭირო ცვლილებები, *როგორ* მოხდა პრობლემის გადაჭრა და
  რა *გვერდითი მოვლენები* შეიძლება მოჰყვეს ამას. 

  It should also provide any pointers to related resources (eg. link to the
  corresponding issue in a bug tracker):
  საგულდაგულო აღწერაში ასევე მოცემული უნდა იყოს ინფორმაცია შესაბამისი რესურსების შესახებ (მაგ. შესაბამისი შეცდომის/პრობლემის (*issue*) ბმული):

  ```text
  Short (50 chars or fewer) summary of changes

  More detailed explanatory text, if necessary. Wrap it to
  72 characters. In some contexts, the first
  line is treated as the subject of an email and the rest of
  the text as the body.  The blank line separating the
  summary from the body is critical (unless you omit the body
  entirely); tools like rebase can get confused if you run
  the two together.

  Further paragraphs come after blank lines.

  - Bullet points are okay, too

  - Use a hyphen or an asterisk for the bullet,
    followed by a single space, with blank lines in
    between

  The pointers to your related resources can serve as a footer
  for your commit message. Here is an example that is referencing
  issues in a bug tracker:

  Resolves: #56, #78
  See also: #12, #34

  Source: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
  ```

  Ultimately, when writing a commit message, think about what you would need
  to know if you run across the commit in a year from now.

* If a *commit A* depends on *commit B*, the dependency should be
  stated in the message of *commit A*. Use the SHA1 when referring to
  commits.

  Similarly, if *commit A* solves a bug introduced by *commit B*, it should
  also be stated in the message of *commit A*.

* If a commit is going to be squashed to another commit use the `--squash` and
  `--fixup` flags respectively, in order to make the intention clear:

  ```shell
  $ git commit --squash f387cab2
  ```

  *(Tip: Use the `--autosquash` flag when rebasing. The marked commits will be
  squashed automatically.)*

## Merging

* **Do not rewrite published history.** The repository's history is valuable in
  its own right and it is very important to be able to tell *what actually
  happened*. Altering published history is a common source of problems for
  anyone working on the project.

* However, there are cases where rewriting history is legitimate. These are
  when:

  * You are the only one working on the branch and it is not being reviewed.

  * You want to tidy up your branch (eg. squash commits) and/or rebase it onto
    the "main" in order to merge it later.

  That said, *never rewrite the history of the "main" branch* or any other
  special branches (ie. used by production or CI servers).

* Keep the history *clean* and *simple*. *Just before you merge* your branch:

    1. Make sure it conforms to the style guide and perform any needed actions
       if it doesn't (squash/reorder commits, reword messages etc.)

    2. Rebase it onto the branch it's going to be merged to:

       ```shell
       [my-branch] $ git fetch
       [my-branch] $ git rebase origin/main
       # then merge
       ```

       This results in a branch that can be applied directly to the end of the
       "main" branch and results in a very simple history.

       *(Note: This strategy is better suited for projects with short-running
       branches. Otherwise it might be better to occassionally merge the
       "main" branch instead of rebasing onto it.)*

* If your branch includes more than one commit, do not merge with a
  fast-forward:

  ```shell
  # good - ensures that a merge commit is created
  $ git merge --no-ff my-branch

  # bad
  $ git merge my-branch
  ```

## Misc.

* There are various workflows and each one has its strengths and weaknesses.
  Whether a workflow fits your case, depends on the team, the project and your
  development procedures.

  That said, it is important to actually *choose* a workflow and stick with it.

* *Be consistent.* This is related to the workflow but also expands to things
  like commit messages, branch names and tags. Having a consistent style
  throughout the repository makes it easy to understand what is going on by
  looking at the log, a commit message etc.

* *Test before you push.* Do not push half-done work.

* Use [annotated tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging#_annotated_tags)
  for marking releases or other important points in the history. Prefer
  [lightweight tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging#_lightweight_tags)
  for personal use, such as to bookmark commits for future reference.

* Keep your repositories at a good shape by performing maintenance tasks
  occasionally:

  * [`git-gc(1)`](http://git-scm.com/docs/git-gc)
  * [`git-prune(1)`](http://git-scm.com/docs/git-prune)
  * [`git-fsck(1)`](http://git-scm.com/docs/git-fsck)

# License

![cc license](http://i.creativecommons.org/l/by/4.0/88x31.png)

This work is licensed under a [Creative Commons Attribution 4.0
International license](https://creativecommons.org/licenses/by/4.0/).

# Credits

Agis Anastasopoulos / [@agisanast](https://twitter.com/agisanast) / http://agis.io
... and [contributors](https://github.com/agis-/git-style-guide/graphs/contributors)!