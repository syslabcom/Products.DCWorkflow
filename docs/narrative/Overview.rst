Overview
========

DCWorkflows provide workflow objects that are fully customizable via the Zope
Management Interface. You can specify the states, and the permissions they
set on content that is in that state, the transitions between those states,
and other things like variables for things that aren't well represented by
states, work lists for reviewers, and scripts to embody complex guards and to
extend pre and post transition behaviour.

The process for creating a workflow runs something
like this:

* Draw a state diagram with the nodes (bubbles) as states and the arcs
  (arrows) as transitions. Remember to consider all the states your content can
  be in, and for each state, consider who should have permission to access and
  change the content. Consider what actions the users will perform to make the
  transitions between states, and not only who will be allowed to perform them,
  but who will be *required* to perform them.

  It's often a good idea to start on paper, then transfer
  the diagram to a digital copy using a diagram/flowchart tool, such as
  'dia', so that you have an image to go with later documentation. This
  process tends to make it easier to spot corner cases before you
  actually create the workflow object.

* Start by creating an example DCworkflow, rather than a new one, as it's
  faster to delete all the states and transitions than it is to create all the
  standard variables that tend to be used by the CMF. [**Note:** Perhaps we
  should have a bare dcworkflow, a workflow with standard variables, and the
  couple of standard examples.]

* In the permissions tab, select all the permissions that you want the
  workflow to govern. These will be dependent on the types of content you'll be
  using with the workflow; 'Access contents information', 'Modify portal
  content', and 'View' are the standard permissions for the default portal
  content types.

* Define any extra variables that you need for information that isn't well
  represented by states. [**Note:** generic examples? I can think of a few that
  could appear in some use cases, but they're all idiosyncratic of particular
  publishing needs]

* Set up the states for your workflow, one for each node in your state
  diagram. Try to stick to the standard names for a publication workflow, as
  some badly behaved products have states like 'published' hardcoded into their
  searches (ie CalendarTool, last I looked) [**Note**: Maybe I should just file
  some bug reports rather than casting aspersions :-)]. Set up the permissions
  on the states now, as well, though see the "State Tab" section for advice.

* Set up any scripts that you will be using in your transitions, such as pre
  and post transition scripts and to handle complex guard conditions. Just set
  up skeletons for now, if you haven't though through all the details.

* Create your transitions from all the arcs on your state diagram. You
  should be able to pick the right destination state as all your states
  are already defined, and set up the right scripts to run, as you've
  defined those as well. It's worth noting that the guard behaviour is
  such that if any guard matches, the transition can occur. You can
  specify more than one permission, role or expression by separating
  them with a semicolon.

* Go back to the states tab and, for each state, set the possible transitions
  from the list of all available transitions in each state.

* Finally, in the work lists tab, create any work lists for any states that
  need them. Work lists are actions that indicate how many objects of a given
  state are present, and usually link to some search page that lists the actual
  object instances. You typically use them to list all the pending content
  waiting for review. Work lists have several unusual behaviours, however, so
  check the specific notes in the "Worklists" section.

By working in this order, you will tend to step through the
creation process one tab at a time, rather than switching back and
forth between them, which tends to be slower and somewhat confusing.
