# PostgreSQL DBA-1 Practice Exam Project: Principal Prompts

I had Claude pull together the prompts used to generate the tests. Claude wasn't able to pull together every single prompt, so this may not work perfectly as a way to reproduce my results. The quoted materials are me. The other writing is Claude answering my need for these prompts.

The prompts below, in order, produced the practice exam project: the exam scope, the exam format, the grading and study-guide cycle, and each exam. They are quoted verbatim from the original conversations. Small talk, side questions and one-off tangents are left out.

Exam numbering follows the file names (`PostgreSQL_DBA1_Practice_Exam_NN.md`).

---

## Exam 01

> Just so we're clear, here are the anticipated subjects in the Certification test:
> https://www.oapg-edu.org/certifications/
>
> What I'd need initially is a random scattering of level appropriate questions based on this knowledge set. The answers would be multiple choice. We'd need a way for you to administer the test (presumably through mark down) and then grade my answers. From there, we'll start generating study guides for the topics I don't know well enough.

Result: 40 questions, 5 per topic across 8 topics (T1 to T8), scattered rather than grouped, with a blank `Answer:` line after each. The answer key was held privately.

> OK. I took Practice Exam 01. Please grade it. From there, any suggested readings based on what I got wrong will be helpful. Let's make sure we're up to date on stuff, but no Version 19 content at all. Otherwise, everything should be oriented towards Version 18.

> Before we run the next test, let me get the basic studying done on the stuff I missed. Please provide, if possible, a set of clickable links. As for the links, the bias should be at all times towards the official PostgreSQL documentation, but if any ancillary, 3rd party, documents or videos are more applicable, include those. Break this down by general topic so I know what I'm working on.

> I'd like you to generate a trim as possible markdown with the goals and instructions of this project that can be fed to each new conversation. I was thinking of starting a new conversation for each new quiz.

Result: a `CLAUDE.md` holding the exam scope, the v18-only rule, the file-naming convention and the grade → log → study-guide cycle. Each later exam was run in a fresh conversation from it.

---

## Exam 02

> In the generated study guide, the Topic 5 supplementary information, both links are bad. Is that old data or are we hallucinating in order to always supply supplementary information? Old data is one thing. We don't have to have supplementary info, so better to skip that than make things up.

> Yeah, go ahead and check Study Guide 01. Can you also update your instructions to ensure we either validate the links provided, or skip providing links if no information is available?

Result: link validation became a standing step in `CLAUDE.md`. Every URL and section number must be verified, or the link is omitted.

---

## Exam 03

> Let's try for another test. A very few repeat questions are acceptable. Let's keep the test relatively tough (train hard, fight easy), but, still within the scope as defined in the open alliance description for a junior PostgreSQL DBA.

> OK. That one might have been too tough. However, let's get it graded.

---

## Exam 04

> **Gap:** Exam 04 was an 80-question exam written by Microsoft Copilot, not generated here. The conversation that brought it in starts after the exam was pasted, so its first prompt is not in the saved history. The next prompt is the one that evaluated it.

> I got this test from CoPilot. Correct me if I'm wrong, but it's pretty focused on minutea isn't it: *(full Copilot exam pasted here)*

Result: the exam was found to over-weight psql backslash-command trivia and to contain answer-key errors (Q54, Q64, Q68).

> For all four quizzes that we've done so far, can you create a markdown of the answer sheets. One document for each quiz, named appropriate to the quiz itself. From here on, probably two more quizzes, we'll see, go ahead and generate the answer file when you generate the study guide. Also, for our existing quizzes, can you remove my answers from the quizzes themselves. We have the grading stored, so it doesn't matter to keep it on the files now. I want to share the questions and answers with others.

> Add those instructions to the claude.md file for this project as well. It currently says keep the answer code secret. It should only keep it secret until after it grades my test. Then it can generate an answer file, same as what you did here.

Result: the workflow became a loop. The key stays secret until grading, then is published as the answer file, and the user's answers are stripped from the exam file.

---

## Exam 05

> Let's try another 80 question quiz to see how my knowledge is holding up.

Result: 80 questions at 10 per topic, scoped to PostgreSQL 18.

> I moved the location of the folder so I can put it all in to source control. Can you clean any answers from Test 5 and create the answer key the same as for the other tests. All in this new folder.

---

## Conclusion

And that's it. If you take the prompts I wrote and combine that with the Claude.md file where I kept instructions for Claude, that's how I built these practice tests.
