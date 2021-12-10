# rexams
R/Exams is great for creating multiple-choice exams, but I found it needed some modifications to do what I needed. The template here (which goes in the "tex" directory of the *exams* package directory) works for me.
### Create an exam in a way that order can be randomized
myexam <- list(c(
  "tstat2.Rnw",
  "ttest.Rnw",
  "relfreq.Rnw",
  "anova.Rnw",
  "cholesky.Rnw"
))

### Print the exam to pdf
examPdf <- exams2pdf(myexam, nsamp = 5, n = 2, name = "exam")

### Randomly select 3 items and print the exam to pdf
examPdf  <- exams2pdf(myexam, nsamp = 3, n = 2, name = "exam")
examNops <- exams2nops(myexam, nsamp = 3, n = 2, name = "exam")

# modify tex template used by R/Exams. This template needs to be in the “tex” directory of the package directory 
\documentclass[10pt]{article}
\usepackage[left=.5in, right=.5in, top=.5in, bottom=.75in]{geometry}

Then I changed the answerlist environment to prevent answer lists from spanning multiple pages:

\newenvironment{answerlist}{\renewcommand{\labelenumi}{(\alph{enumi})}\begin{samepage}\begin{enumerate}[topsep=0pt,itemsep=-1ex,partopsep=1ex,parsep=1ex]}{\end{enumerate}\end{samepage}}

answer sheet as a scoring sheet (i.e., something that shows a list of correct answers). So I changed this line:

\newcommand{\extext}[1]{\phantom{\large #1}} to this one: \newcommand{\extext}[1]{\textbf{\large #1}}

% Remove by comments to aoid answers
%% \exinput{questionnaire}

So now the final command that I run to get the exams, formatted the way I want them is:

finalExam <- exams2pdf(myexam, n = 2, nsamp = 5, name = "finalExam", template="myexam2")

% modifications from https://deskreject.com/2019/01/r-exams/
