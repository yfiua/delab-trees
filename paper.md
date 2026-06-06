---
title: 'delab-trees: A Python library for analysing conversation reply trees in social media research'
tags:
  - Python
  - social media analysis
  - conversation analysis
  - deliberation
  - reply trees
  - computational social science
authors:
  - name: Julian Dehne
    orcid: 0000-0001-9265-9619
    affiliation: 1
affiliations:
  - name: University of Göttingen, Germany
    index: 1
date: 13 May 2026
bibliography: paper.bib
---

# Summary

`delab-trees` is a Python library for analysing conversational reply trees as they
arise in social-media platforms (Twitter, Reddit, Mastodon) and online discussion
fora. It treats a *conversation* as a directed reply graph rooted in an opening post,
exposes both a tabular (`pandas.DataFrame`) and a graph (`networkx.DiGraph`)
representation of that conversation, and provides a uniform API for: validating tree
structure, extracting *conversation flows* (root-to-leaf paths through the reply
graph), computing author-centrality metrics, comparing flows by quantitative content
features, and (experimentally) training simple neural models for participation-aware
author scoring.
The library is designed to operate on a single shared input schema (`tree_id`,
`post_id`, `parent_id`, `author_id`, `text`, `created_at`) so that data drawn from
different platforms can be analysed with identical code paths.

Two core abstractions structure the library: `TreeManager` holds a dictionary of
trees keyed by `tree_id`, and `DelabTree` represents a single conversation, carrying
its `pandas.DataFrame` form alongside a `networkx` reply graph. A `DelabTree` can be
projected into derived graphs (author graph, author-interaction graph, recursive
tree), cleaned (cycle removal, orphan attachment, merging consecutive same-author
posts), filtered (largest connected component, flows of a given length), and scored
(branching weight, depth, root dominance, betweenness/closeness/Katz centrality per
author).

# Statement of need

Research on online conversations in computational social science is dominated by
post-centric or user-centric measures: counts of replies, follower-network influence,
sentiment of individual posts. These quantitative reductions overlook the
*structural* dimension of online conversations — the shape of the reply tree and the
position of authors within it — which carries information about deliberative quality
that text-level analysis cannot recover [@Magnani2012; @Aragon2017].

Several lines of work argue that the conversation *structure* is itself a meaningful
unit of analysis: reply trees and the implicit thread structures that recover them
[@Wang2008], branching-process models of Twitter conversations [@Nishi2016], graph
reconstruction of Twitter conversation graphs [@Cogan2012], and meso-/macro-level
conversation structures in support forums [@Joglekar2020]. What has been missing is a
reusable Python library that takes the *conversation flow* (root-to-leaf path) as a
first-class object and supports research questions about deliberation, moderation,
and participation at that granularity.

`delab-trees` fills this gap. It provides:

- A platform-agnostic representation of reply trees from a minimal schema, so that
  Reddit, Twitter, Mastodon and forum data can be analysed under one API.
- Conversation-flow extraction with optional filtering by length and predicate.
- `FlowDuo`, a routine for finding the two flows within a conversation with the
  largest contrast on a chosen content metric (e.g. sentiment) — useful for selecting
  illustrative cases or constructing matched comparisons.
- Experimental, participation-aware author-scoring models that aim to go beyond raw
  centrality: a *response-based* (RB) classifier that learns whether an author has
  likely seen a post from reply-distance features, and a *prediction-based* (PB) model
  that scores authors by their predictability as the next contributor given
  conversation context [@Dehne2023cccp]. These two models are provided as a research
  prototype and are still under active development; the stable, tested core of the
  library is the reply-tree representation, conversation-flow extraction, `FlowDuo`,
  and the centrality metrics described above.

# Use cases

`delab-trees` is the shared substrate for several recent studies of deliberation in
online discussion. It supports the conversation-flow unit of analysis in a
large-scale empirical study of user moderation on Twitter, where reply-tree
reconstruction and flow extraction are upstream of every downstream model
[@Dehne2024moderation]. It implements the participation metrics evaluated in the
CCCP study comparing Reddit and Twitter [@Dehne2023cccp]. And it underpins the
intervention-recovery procedure in a deployed-bot study on Reddit and Mastodon,
where deleted bot posts are matched back into recovered reply trees in order to
preserve the empirical record for analysis [@Dehne2024delabbot]. The library is
distributed via PyPI (`pip install delab_trees`) and ships with anonymised Reddit
and Twitter example datasets for reproduction of the published results.

# Acknowledgements

The work on `delab-trees` was conducted in the context of research on deliberation
and moderation in social media at the University of Göttingen. The author thanks
collaborators on the connected empirical studies for feedback that shaped the API.

# References
