# Git Style Guide
# Git-ის სტილისტიკის სახელმძღვანელო

# Table of contents
## სარჩევი

1. [განშტოებები](#branches)
2. [ქომითები](#commits)
    - [შეტყობინებები](#messages)
3. [შერწყმა](#merging)
4. [სხვადასხვა](#misc)
5. [ლიცენზია](#license)

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
* განშტოებათა სახელის ჩაწერისათვის გამოიყენეთ პატარა ასოები. გარე სერვისთა იდენტიფიკატორების დიდი ასოებით ჩაწერა დასაშვები გამონაკლისია.
  სიტყვების ერთმანეთისაგან გამოსაყოფად გამოიყენეთ ტირეები.

  ```shell
  $ git checkout -b new-feature      # good # კარგია
  $ git checkout -b T321-new-feature # good (Phabricator task id) # კარგია (Phabricator task id)
  $ git checkout -b New_Feature      # bad # ცუდია
  ```

* When several people are working on the *same* feature, it might be convenient
  to have *personal* feature branches and a *team-wide* feature branch.
  Use the following naming convention:
* როდესაც *ერთსა და იმავე* ფუნქციონალზე რამდენიმე ადამიანი მუშაობს, შესაძლოა მოსახერხებელი იყოს,
  თუკი თითოეულისათვის გამოყოფილი ექნება *პირადი* განშტოება და ცალკე იქნება გამოყოფილი *მთელი გუნდისათვის საერთო* განშტოება.
  გამოიყენეთ სახელდების შემდეგი კანონზომიერება:

  ```shell
  $ git checkout -b feature-a/main   # team-wide branch  # მთელი გუნდისათვის საერთო განშტოება
  $ git checkout -b feature-a/maria  # Maria's personal branch # მარიას პირადი განშტოება
  $ git checkout -b feature-a/nick   # Nick's personal branch # ნიკის პირადი განშტოება
  ```

  Merge at will the personal branches to the team-wide branch (see ["Merging"](#merging)).
  Eventually, the team-wide branch will be merged to "main".
  სურვილისამებრ, მოახდინეთ პირად განშტოებათა შერწყმა მთელი გუნდისათვის საერთო განშტოებასთან (იხ. [„შერწყმა“](#merging)).
  საბოლოოდ, მოხდება მთელი გუნდისათვის საერთო განშტოების შერწყმა მთავარ („main“) განშტოებასთან.

* Delete your branch from the upstream repository after it's merged, unless
  there is a specific reason not to.

  Tip: Use the following command while being on "main", to list merged
  branches:
* შერწყმის შემდეგ წაშალეთ განშტოება,
  თუკი არ გაქვთ მისი არწაშლის კონკრეტული მიზეზი.

  რჩევა: გაუშვით შემდეგი ბრძანება მთავარ („main“) განშტოებაზე ყოფნისას,
  რათა იხილოთ [მასთან] შერწყმულ განშტოებათა სია:

  ```shell
  $ git branch --merged | grep -v "\*"
  ```

## Commits
## ქომითები (Commits)

* Each commit should be a single *logical change*. Don't make several
  *logical changes* in one commit. For example, if a patch fixes a bug and
  optimizes the performance of a feature, split it into two separate commits.

  *Tip: Use `git add -p` to interactively stage specific portions of the
  modified files.*
* თითოეული ქომითი უნდა წარმოადგენდეს ერთ *ლოგიკურ ცვლილებას*. ნუ გააერთიანებთ რამდენიმე *ლოგიკურ ცვლილებას* ერთ ქომითში.
  მაგალითად, თუ გამოასწორეთ ხარვეზი და გააუმჯობესეთ წარმადობა,
  უმჯობესია, ცვლილებები დაყოთ ორ დამოუკიდებელ ქომითად.

  *რჩევა: გამოიყენეთ `git add -p` [ბრძანება] მოდიფიცირებულ ფაილთა ცალკეული ნაწილების
  ინტერაქტიულად ორგანიზებისათვის.*

* Don't split a single *logical change* into several commits. For example,
  the implementation of a feature and the corresponding tests should be in the
  same commit.
* არ დაყოთ ერთი *ლოგიკური ცვლილება* რამდენიმე ქომითად. მაგალითად,
  ფუნქციონალის რეალიზაცია და [მისთვის] სათანადო ტესტები უნდა გაერთიანდეს ერთსა და იმავე
  ქომითში.

* Commit *early* and *often*. Small, self-contained commits are easier to
  understand and revert when something goes wrong.
* განახორციელეთ ქომითები *დროულად* და *ხშირად*. მოკლე, თვითმყოფადი ქომითები მეტად მარტივად გასაგებია და
  ამარტივებს უწინდელ მდგომარეობაში დაბრუნებას, თუკი რაიმე არასწორად წარიმართება.

* Commits should be ordered *logically*. For example, if *commit X* depends
  on changes done in *commit Y*, then *commit Y* should come before *commit X*.
* ქომითები *ლოგიკური* თანმიმდევრობით უნდა განხორციელდეს. მაგალითად, თუ *X-ქომითი* დამოკიდებულია
  *Y-ქომითში* განხორციელებულ ცვლილებებზე, მაშინ *Y-ქომითი* უნდა განხორციელდეს *X-ქომითამდე*.

Note: While working alone on a local branch that *has not yet been pushed*, it's
fine to use commits as temporary snapshots of your work. However, it still
holds true that you should apply all of the above *before* pushing it.
შენიშვნა: ვიდრე მარტოდმარტო მუშაობთ ადგილობრივ (*ლოკალურ*) განშტოებაზე, *რომლის ატვირთვაც (push) ჯერ არ მომხდარა*,
დასაშვებია ქომითების, როგორც თქვენი სამუშაოს დროებითი ჩანაწერების, გამოყენება. თუმცა,
ისევ და ისევ მართებულია ზემოთ მოყვანილი რეკომენდაციების დაცვა, *სანამ* ატვირთვას მოახდენდეთ.

### Messages
### შეტყობინებები (Messages)

* Use the editor, not the terminal, when writing a commit message:
* ქომითის აღწერისას გამოიყენეთ რედაქტორი, და არა ბრძანებათა სტრიქონი (*ტერმინალი*):

  ```shell
  # good # კარგია
  $ git commit

  # bad # ცუდია
  $ git commit -m "Quick fix"
  ```

  Committing from the terminal encourages a mindset of having to fit everything
  in a single line which usually results in non-informative, ambiguous commit
  messages.
  ქომითისათვის ბრძანებათა სტრიქონის (*ტერმინალის*) გამოყენება გზღუდავთ, გიწევთ ყველაფრის ერთ ხაზში ჩატევა,
  რაც, ჩვეულებრივ, შეტყობინებებს არაინფორმაციულსა და
  ბუნდოვანს ხდის.

* The summary line (ie. the first line of the message) should be
  *descriptive* yet *succinct*. Ideally, it should be no longer than
  *50 characters*. It should be capitalized and written in imperative present
  tense. It should not end with a period since it is effectively the commit
  *title*:
* სათაური (ანუ შეტყობინების პირველი ხაზი) უნდა იყოს
  *აღწერითი*, მაგრამ *ლაკონიური*. იდეალურ შემთხვევაში, იგი უნდა შედგებოდეს
  არაუმეტეს *50 სიმბოლოსაგან*. ჩანაწერი უნდა იწყებოდეს დიდი ასოთი და დაიწეროს აწმყო დროში, იმპერატიულად.
  [წინადადების] ბოლოს წერტილს ნუ დასვამთ, რადგან, ფაქტობრივად *სათაურს* წერთ:

  ```shell
  # good - imperative present tense, capitalized, fewer than 50 characters # კარგია - აწმყო დროშია, იმპერატიულია, დიდი ასოთი იწყება, შედგება 50-ზე ნაკლები სიმბოლოსაგან
  Mark huge records as obsolete when clearing hinting faults

  # bad # ცუდია
  fixed ActiveModel::Errors deprecation messages failing when AR was used outside of Rails.
  ```

* After that should come a blank line followed by a more thorough
  description. It should be wrapped to *72 characters* and explain *why*
  the change is needed, *how* it addresses the issue and what *side-effects*
  it might have.
* შემდგომ ამისა უნდა მოდიოდეს ცარიელი სტრიქონი, რომელსაც მოსდევს უფრო საგულდაგულო აღწერა.
  აღწერა უნდა შედგებოდეს [არაუმეტეს] *72 სიმბოლოსაგან* და უნდა განმარტავდეს,
  თუ *რატომ* იყო საჭირო ცვლილებები, *როგორ* მოხდა პრობლემის გადაჭრა და
  რა *გვერდითი მოვლენები* შეიძლება მოჰყვეს ამას.

  It should also provide any pointers to related resources (eg. link to the
  corresponding issue in a bug tracker):
  საგულდაგულო აღწერაში ასევე მოცემული უნდა იყოს ინფორმაცია გამოყენებული რესურსების შესახებ
  (მაგ. შესაბამისი შეცდომის/პრობლემის (*issue*) ბმული):

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
  მარტივად რომ ვთქვათ, როდესაც ქომითის შეტყობინებას წერთ, უნდა დაფიქრდეთ იმაზე,
  თუ რისი ცოდნა შეიძლება დაგჭირდეთ, თუკი ამ ქომითს ერთ წელიწადში წააწყდებით.

* If a *commit A* depends on *commit B*, the dependency should be
  stated in the message of *commit A*. Use the SHA1 when referring to
  commits.

  Similarly, if *commit A* solves a bug introduced by *commit B*, it should
  also be stated in the message of *commit A*.
* თუკი *A-ქომითი* დამოკიდებულია *B-ქომითზე*,
  ეს დამოკიდებულება უნდა აღიწეროს *A-ქომითის* შეტყობინებაში.
  *ქომითებზე მითითებისას გამოიყენეთ SHA1-ჰეში*.

  ანალოგიურად, თუ *A-ქომითი* წყვეტს *B-ქომითის* მიერ წარმოქმნილ პრობლემას,
  ამის ფორმულირებაც *A-ქომითის* შეტყობინებაში უნდა მოხდეს.

* If a commit is going to be squashed to another commit use the `--squash` and
  `--fixup` flags respectively, in order to make the intention clear:
* თუკი ქომითი უნდა გაერთიანდეს (*squash*) სხვა ქომითთან, გამოიყენეთ `--squash` და
  `--fixup` არგუმენტები სათანადოდ, რათა [თქვენი] მიზანი უფრო ნათელი გახადოთ:

  ```shell
  $ git commit --squash f387cab2
  ```

  *(Tip: Use the `--autosquash` flag when rebasing. The marked commits will be
  squashed automatically.)*
  (რჩევა: რებაზირების (*rebasing*) დროს გამოიყენეთ `--autosquash` არგუმენტი.
  [ამით,] მონიშნული ქომითები ავტომატურად გაერთიანდება.)

## Merging
## შერწყმა (Merging)

* **Do not rewrite published history.** The repository's history is valuable in
  its own right and it is very important to be able to tell *what actually
  happened*. Altering published history is a common source of problems for
  anyone working on the project.
* **ნუ მოახდენთ გამოქვეყნებული ისტორიის გადამუშავებას.** საცავის (*repository*) ისტორია თავისთავად ღირებულია, და
  ძალიან მნიშვნელოვანია შეგეძლოთ დანახვა იმისა, *თუ რა მოხდა სინამდვილეში*.
  გამოქვეყნებული ისტორიის ცვლილება პრობლემათა გავრცელებული წყაროა ყველასთვის,
  ვინც პროექტზე მუშაობს.

* However, there are cases where rewriting history is legitimate. These are
  when:
* თუმცა, არსებობს შემთხვევები, როდესაც ისტორიის გადამუშავება ლეგიტიმურია.
  მაგალითად:

  * You are the only one working on the branch and it is not being reviewed.
  * როდესაც განშტოებაზე მხოლოდ თქვენ მუშაობთ და მისი (განშტოების) განხილვა არ მოხდება.

  * You want to tidy up your branch (eg. squash commits) and/or rebase it onto
    the "main" in order to merge it later.
  * როდესაც გსურთ, რომ მოაწესრიგოთ თქვენი განშტოება (მაგ. გააერთიანოთ ქომითები) ან/და ახდენთ მის რებაზირებას
    „main“ განშტოებაზე, რათა მოგვიანებით მოახდინოთ [მათი] შერწყმა.

  That said, *never rewrite the history of the "main" branch* or any other
  special branches (ie. used by production or CI servers).
  როგორც ითქვა, *არასოდეს შეიტანოთ ცვლილება „main“ განშტოების*, ან ნებისმიერი სხვა
  სპეციალური დანიშნულების მქონე (მაგალითად, CI-სერვერების მიერ გამოყენებული) განშტოებების ისტორიაში.

* Keep the history *clean* and *simple*. *Just before you merge* your branch:
* შეინარჩუნეთ ისტორიის *სისუფთავე* და *სიმარტივე*. ვიდრე განშტოების შერწყმას მოახდენდეთ:

    1. Make sure it conforms to the style guide and perform any needed actions
       if it doesn't (squash/reorder commits, reword messages etc.)
    1. დარწმუნდით, რომ იგი შეესაბამება წინამდებარე სახლემძღვანელოს მითითებებს; ხოლო თუ ეს ასე არ არის, შეასრულეთ ნებისმიერი საჭირო მოქმედება
       (გააერთიანეთ ქომითები ან შეცვალეთ მათი თანმიმდევრობა, ხელახლა უზრუნველყავით შეტყობინებები და სხვ.).

    2. Rebase it onto the branch it's going to be merged to:
    2. მოახდინეთ მისი რებაზერიბა იმ განშტოებაზე, რომელთანაც შემდგომში მისი შერწყმა უნდა მოხდეს:

       ```shell
       [my-branch] $ git fetch
       [my-branch] $ git rebase origin/main
       # then merge # შემდგომ ამისა, მოახდინეთ შერწყმა
       ```

       This results in a branch that can be applied directly to the end of the
       "main" branch and results in a very simple history.
       შედეგად ვიღებთ ძალიან მარტივ ისტორიას და განშტოებას,
       რომელიც შესაძლებელია გამოყენებულ იქნეს უშუალოდ „main“ განშტოების ბოლოში.

       *(Note: This strategy is better suited for projects with short-running
       branches. Otherwise it might be better to occassionally merge the
       "main" branch instead of rebasing onto it.)*
       *(შენიშვნა: ეს მეთოდი უკეთ შეეფერაბა მოკლევადიანი განშტოებებისაგან შემდგარ პროექტებს.
       სხვა შემთხვევებში შესაძლოა უმჯობესი იყოს, პერიოდულად მოახდინოთ „main“ განშტოების შერწყმა,
       ნაცვლად მასზე რებაზირებისა.)*

* If your branch includes more than one commit, do not merge with a
  fast-forward:
* თუკი თქვენი განშტოება შეიცავს ერთზე მეტ ქომითს, არ მოახდინოთ შერწყმა
  დაჩქარებულად (*fast-forward*):

  ```shell
  # good - ensures that a merge commit is created # კარგია - იძლევა გარანტიას, რომ შერწყმის ქომითი შეიქმნა
  $ git merge --no-ff my-branch

  # bad # ცუდია
  $ git merge my-branch
  ```

## Misc.
## სხვადასხვა (Misc.)

* There are various workflows and each one has its strengths and weaknesses.
  Whether a workflow fits your case, depends on the team, the project and your
  development procedures.

  That said, it is important to actually *choose* a workflow and stick with it.
* არსებობს მთელი რიგი შრომითი პროცესები (*workflows*) და თითოეულს გააჩნია თავისი ძლიერი და სუსტი მხარეები.
  შეესაბამება თუ არა ესა თუ ის შრომითი პროცესი თქვენს შემთხვევას დამოკიდებულია თქვენს გუნდზე, პროექტზე და დეველოპმენტის
  თქვენებურ მეთოდიკაზე.

  ასე რომ, მნიშვნელოვანია *შეარჩიოთ* შრომითი პროცესი (*workflow*) და გულმოდგინეთ მიჰყვეთ მას.

* *Be consistent.* This is related to the workflow but also expands to things
  like commit messages, branch names and tags. Having a consistent style
  throughout the repository makes it easy to understand what is going on by
  looking at the log, a commit message etc.
* *იყავით თანმიმდევრული.* ეს შრომით პროცესს ეხება, მაგრამ ასევე ვრცელდება ისეთ საკითხებზე,
  როგორიცაა - ქომითის შეტყობინებები, განშტოებათა სახელები და ტეგები.
  საცავის მასშტაბით თანმიმდევრული სტილის არსებობა
  გაგიმარტივებთ სამუშაოს პროგრესის იდენტიფიცირებას.

* *Test before you push.* Do not push half-done work.
* *მოახდინეთ ტესტირება, ვიდრე ატვირთავთ.* ნუ ატვირთავთ სანახევროდ შესრულებულ ნამუშევარს.

* Use [annotated tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging#_annotated_tags)
  for marking releases or other important points in the history. Prefer
  [lightweight tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging#_lightweight_tags)
  for personal use, such as to bookmark commits for future reference.
* გამოიყენეთ [ანოტირებული ტეგები](https://git-scm.com/book/en/v2/Git-Basics-Tagging#_annotated_tags) გამოშვებათა (*releases*) ან 
  სხვა მნიშვნელოვანი პუნქტების ისტორიაში აღნიშვნისათვის.
  უპირატესობა მიანიჭეთ [მსუბუქ ტეგებს](https://git-scm.com/book/en/v2/Git-Basics-Tagging#_lightweight_tags) პირადი გამოყენებისათვის,
  როგორიცაა ქომითების ჩანიშვნა სამომავლო მითითებისათვის (*reference*).

* Keep your repositories at a good shape by performing maintenance tasks
  occasionally:
* თქვენი საცავების კარგ ფორმაში შენარჩუნებისათვის პერიოდულად შეასრულეთ
  მოვლით-შენახვითი სამუშაოები:

  * [`git-gc(1)`](http://git-scm.com/docs/git-gc)
  * [`git-prune(1)`](http://git-scm.com/docs/git-prune)
  * [`git-fsck(1)`](http://git-scm.com/docs/git-fsck)

## License
## ლიცენზია

![cc license](http://i.creativecommons.org/l/by/4.0/88x31.png)

This work is licensed under a [Creative Commons Attribution 4.0
International license](https://creativecommons.org/licenses/by/4.0/).
