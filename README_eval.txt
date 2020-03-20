	    TAC 2008 Update Summarization Task: Evaluation Results
	    ======================================================


This is the README file for the manual and automatic evaluation that
was performed at NIST for summaries in the TAC 2008 update
summarization task.

Eight NIST assessors selected and wrote summaries for the 48 topics in
the TAC 2008 update summarization task.  Each topic had 2 docsets
(A,B), and 4 human summaries were written for each docset.  The human
summarizer IDs are A-H.

NIST received 71 runs from 33 participants for the update
summarization task.  The participants each submitted up to three runs,
ranked by priority.  NIST evaluated all runs automatically using
ROUGE/BE.  NIST provided manual evaluations only for runs with
priority 1 and 2. The participants' summarizer IDs are 1-71 in the
ROUGE/BE evaluations, and 1-57 in the manual evaluations.

In addition, one baseline summarizer was included in the evaluation:

    Baseline (summarizer ID = 0): return all the leading sentences (up
    to 100 words) in most recent document.

All summaries were truncated to 100 words before being evaluated.
Summaries are saved one per file, using the following naming
convention: <topic-docset>.M.100.<topic_selectorID>.<summarizerID>



Manual Evaluation
-----------------

The manual evaluation comprised the following:

    1. Pyramid-based evaluation of content 
    2. assessment of linguistic quality
    3. assessment of overall responsiveness.

Pyramid Content: NIST assessors created Pyramids from the 4 model
summaries for each docset, and annotated peer summaries using the
guidelines in:
   http://www1.cs.columbia.edu/~becky/DUC2006/2006-pyramid-guidelines.html
Four 3-model pyramids were then derived from each 4-model pyramid in
order to implement jackknifing and compare pyramid scores for systems
and humans.

Linguistic Quality: NIST assessors assigned an overall linguistic
quality score to each of the automatic and human summaries.  The score
is an integer between 1 (very poor) and 5 (very good) and is guided by
consideration of the following factors:

	1. Grammaticality
	2. Non-redundancy
	3. Referential clarity
	4. Focus
	5. Structure and Coherence

Overall Responsiveness: NIST assessors assigned an overall
responsiveness score to each of the automatic and human summaries.
The overall responsiveness score is an integer between 1 (very poor)
and 5 (very good) and is based on both the linguistic quality of the
summary and the amount of information in the summary that helps to
satisfy the information need expressed in the topic narrative.

Files under manual/:
   peers/			automatic summaries (Pyramid annotation format)
   models/			model summaries (text format)
   pyramids/			Pyramids for each topic (.pyr files)
   manual.peer			peer scores table (see MANUAL.PEER below)
   manual.model			model scores table (see MANUAL.MODEL below)
   manual.peer.avg		average scores per summarizer (see MANUAL.PEER.AVG below)
   manual.model.avg		average scores per summarizer (see MANUAL.MODEL.AVG below)
   topic_per_assessor.txt	assessor codes and the topics that each assessor annotated


MANUAL.PEER table

Columns in the peer results table contain the following information:

1. setID---document set ID
2. peerID---peer summarizer ID

3. modified (pyramid) score---this score equals the sum of the weights
       of the Summary Content Units (SCUs) that a peer summary
       matches, normalized by the ideal weight of a summary which has
       the same number of contributors as the average of the 4 model
       summaries in the associated pyramid.
4. numSCUs---the number of unique contributors in the peer summary
       that match an SCU in the model pyramid. Note that a pyramid SCU
       can be matched by more than one contributor, in the case of
       exact or paraphrase repetition.
5. numrepetitions---the number of contributors in the peer that
       repeated a match to a pyramid SCU. For each set of contributors
       in the peer summary that match the same pyramid SCU, only one
       increments the count in column 4. The rest appear in this
       field; thus the total number of contributing content units in a
       peer summary would be given by summing columns 4 and 5.
       (HOWEVER: NIST assessors were told that it was sufficient for
       scoring purposes to mark just one contributor for each SCU that
       was matched, although they were encouraged to mark any
       additional contributors.)
6. annotator---the ID for the assessor who created the pyramid and
       annotated all machine summaries for the given docset against it.
7. average modified score with 3 models---this score is also a
       modified (pyramid) score as in column 3, but in this case it 
       is the average of four scores, each calculated with only three 
       model summaries (instead of all four), in all possible combinations.
8. linguistic quality---overall linguistic quality of the peer summary
9. overall---the overall responsiveness judgment for the peer summary


MANUAL.MODEL TABLE

Columns in the model results table contain the following information:

1. setID---document set ID
2. modelID---human summarizer ID
3. numSCUs---the number of unique contributors in the human summary
       that match an SCU in the model pyramid (which is constructed
       from the remaining 3 model summaries for that document
       set).
4.annotator---the ID for the assessor who created the pyramid and
       annotated all machine summaries for a given set against it. 
5. modified (pyramid) score---calculated against the pyramid
   constructed from the remaining 3 models. As in the case of peer
   evaluation, this score equals the sum of the weights of the Summary
   Content Units (SCUs) that a summary matches, normalized by the
   ideal weight of a summary which has the same number of contributors
   as the average of the 3 model summaries in the associated pyramid.
6. linguistic quality---overall linguistic quality of the human summary
7. overall---the overall responsiveness judgment for the human summary


MANUAL.PEER.AVG TABLE

Columns in the average peer results table present scores for each run
averaged over all topics. The table contains the following information
(descriptions of columns correspond to the MANUAL.PEER TABLE):

1. peerID
2. average modified (pyramid) score
3. average numSCUs
4. average numrepetitions
5. macroaverage modified score with 3 models
6. average linguistic quality
7. average overall responsiveness


MANUAL.MODEL.AVG TABLE

Columns in the average model results table present scores for each
human summarizer (A-H) averaged over all relevant topics (i.e. all
summaries they created). The table contains the following information
(descriptions of columns correspond to the MANUAL.MODEL TABLE):

1. modelID
2. average numSCUs
3. average modified (pyramid) score against the remaining 3 models
4. average linguistic quality
5. average overall responsiveness



ROUGE
-----

ROUGE-2 and ROUGE-SU4 scores were computed by running ROUGE-1.5.5 with
stemming but no removal of stopwords.  The input file rougejk.in implemented
jackknifing so that scores of systems and humans could be compared. 

ROUGE run-time parameters:
   ROUGE-1.5.5.pl -n 4 -w 1.2 -m  -2 4 -u -c 95 -r 1000 -f A -p 0.5 -t 0 -a -d rouge.in 
   ROUGE-1.5.5.pl -n 4 -w 1.2 -m  -2 4 -u -c 95 -r 1000 -f A -p 0.5 -t 0 -a -d rougejk.in 

Files under ROUGE/:
   models/		sentence-segmented human summaries
   peers/		sentence-segmented automatic summaries
   rouge.in		input file to ROUGE-1.5.5		
   rouge.m.out		output of ROUGE-1.5.5
   rouge2.m.avg		average ROUGE-2 recall, by summarizer ID
   rougeSU4.m.avg	average ROUGE-SU4 recall, by summarizer ID
   rougejk.in		input file to ROUGE-1.5.5 (with jackknifing)
   rougejk.m.out	output of ROUGE-1.5.5 (with jackknifing)
   rouge2.jk.m.avg	average ROUGE-2 recall, by summarizer ID (with jackknifing)
   rougeSU4.jk.m.avg	average ROUGE-SU4 recall, by summarizer ID (with jackknifing)



Basic Elements
--------------

Basic Elements (BE) scores were computed by first using the tools in
BE-1.1 to extract BE-F from each sentence-segmented <summary>:
   bebreakMinipar.pl -p $MINIPATH <summary>

The BE-F were then matched by running ROUGE-1.5.5 with stemming, using
the Head-Modifier (HM) matching criterion.  The input file simplejk.in
implemented jackknifing so that scores of systems and humans could be
compared.

BE run-time parameters:
   ROUGE-1.5.5.pl -m -a -d -3 HM simple.in  
   ROUGE-1.5.5.pl -m -a -d -3 HM simplejk.in  

Files under BE/:
   BEmodels/			BEs from human summaries
   BEpeers/			BEs from automatic summaries
   simple.in			input file to ROUGE-1.5.5
   simple.m.hm.out		output of ROUGE-1.5.5
   simple.m.hm.avg		average BE recall, by summarizer ID
   simplejk.in			input file to ROUGE-1.5.5 (with jackknifing)
   simplejk.m.hm.out		output of ROUGE-1.5.5 (with jackknifing)
   simple.jk.m.hm.avg		average BE recall, by summarizer ID (with jackknifing)
