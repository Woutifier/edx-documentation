.. _drag_and_drop_problem:

##########################
Drag and Drop Problem
##########################

In drag and drop problems, learners respond to a question by dragging text or
objects to a specific location on an image. This section explains how to use
drag and drop problems in your course.

.. contents::
  :local:
  :depth: 1

.. note:
    This drag and drop problem type is intended as a replacement for an older
    drag and drop problem type. This drag and drop problem type includes
    significant improvements and you should use it for any new course
    development. For more information about the previous, deprecated drag and
    drop problem type, see :ref:`Drag and Drop`.

.. _overview_of_drag_and_drop_problems:

**********************************
Overview of Drag and Drop Problems
**********************************

A drag and drop problem includes a background image and one or more draggable
images that learners move into target zones on the background image. You can
include as many draggable items and as many target zones as you need. You can
include decoy items that do not have a target and you can include decoy targets
that do not correspond to draggable items.

Learners drag items from the top section of the drag and drop problem on to the
background image. The way that a learner selects, or grabs, an item depends on
the type of browser that that learner uses. For example, a learner might click
and hold on a draggable item with a mouse pointer to select it, drag the item
to a target, and release the mouse pointer to drop the item on the target. The
drag and drop problem type supports mobile device interfaces. If a learner
requires or prefers a keyboard interface, the drag and drop problem type
supports selecting items and their matching target zones with standard keyboard
navigation keys for a web browser.

Learners will receive full credit for a drag and drop problem when all items
that have matching zones have been dragged to those zones. Drag and drop
problems do not support partial credit.

The following image shows an example drag and drop problem.

.. image:: ../../../shared/images/dnd-initial.png
  :width: 600
  :alt: An example of a simple drag and drop problem. The components of the
      problem, such as its title, text, and introductory feedback are labeled.

The following image shows the success feedback message that learners see when
they match a draggable item with its target zone. Each draggable item has its
own success feedback message.

.. image:: ../../../shared/images/dnd-correct-feedback.png
  :width: 400
  :alt: An example of a simple drag and drop problem. The success feedback
      message appears above the background image.

The following image shows the error feedback message that learners see when
they match a draggable item with an incorrect target zone. Each draggable item
has its own error feedback message.

.. image:: ../../../shared/images/dnd-incorrect-feedback.png
  :width: 400
  :alt: An example of a simple drag and drop problem. The error feedback
      message appears over the background image.

The following image shows a completed drag and drop problem. The final feedback
message informs the learner that the problem is complete.

.. image:: ../../../shared/images/dnd-complete.png
  :width: 400
  :alt: An example of a simple drag and drop problem. The problem is complete
      and the final feedback message appears below the background image.


===============================
Understanding Background Images
===============================

The background image for a drag and drop problem is the surface that learners
drag items onto.

A target zone is a rectangular area on the background image. You can display or
hide the borders of a zone for learners. You can add labels for zones or leave
them unlabeled.

A background image must fit within the course screen and the LMS will scale
images that are too wide. If you choose a background image that is extremely
large, you should consider how it will appear to learners after scaling. The
width of the course screen depends on the device and browsing software that a
learner uses.

You define target zones by specifying their width, height, horizontal offset
(``x``), and vertical offset (``y``). Each specification is in pixels. The
horizontal offset is the distance between the left side of the background image
and the left side of the target zone. The vertical offset is the distance
between the top of the background image and the top of the target zone.

The following image shows a background image and target zones in the drag and
drop problem editing dialog box. For information about editing drag and drop
problems, see :ref:`creating_a_drag_and_drop_problem`.

.. image:: ../../../shared/images/dnd-zone-borders.png
  :width: 600
  :alt: A background image and target zones shown in the drag and drop problem
      editing dialog box.

==============================
Understanding Draggable Items
==============================

A draggable item is a rectangle that contains either a label or an image.
Learners will grab droppable items from the top of a drag and drop problem and
drag them to targets on the background image.

The size of the rectangle depends on the amount or text in the label or the
size of the image. You can set the background color and the label text color
for the items in a problem.

Each draggable item can match one target zone on the background image. A
draggable item can match none of the target zones.

Each item must have a text label to identify it in the drag and drop problem.
If you include only a text label, that label appears in the draggable item. If
you include both a text label and an image for an item, the image appears as
its label.

The following image shows draggable items with image labels. For examples of
items with text labels, see :ref:`overview_of_drag_and_drop_problems`.

.. image:: ../../../shared/images/dnd-draggable-item-images.png
  :width: 400
  :alt: Draggable items with image labels in the item area of a drag and drop
      problem.

Image labels for draggable items have alternate image descriptions. The
alternate description explains the image content in text. If a learner cannot
access the visual image content, the text description helps that learner to
complete the problem.

.. note::
    If an image file is unavailable, or cannot be displayed, the LMS will
    display the text description as the button label.

.. _enabling_drag_and_drop_problem:

*********************************
Enabling Drag and Drop Problems
*********************************

.. _creating_a_drag_and_drop_problem:

*********************************
Creating a Drag and Drop Problem
*********************************

To create a drag and drop problem, you

.. _changing_visual_style_of_drag_and_drop_problem:

****************************************************
Changing the Visual Style of a Drag and Drop Problem
****************************************************

You can change the visual appearance of drag and drop problems in your courses. You can change the appearance of the draggable items in an individual problem or


