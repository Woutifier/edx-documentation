.. _styling_drag_and_drop_problems:

##############################
Styling Drag and Drop Problems
##############################

You can customize the appearance of drag and drop problems in your Open edX
site by adding a Python programming language module and a Cascading Style Sheet
(CSS) file. The style that you configure applies to all drag and drop problems
in all courses. For more information about drag and drop problems, see
:ref:`opencoursestaff:drag_and_drop_problem`.

.. note::
    You can also style the background and text colors of the draggable items in
    an individual drag and drop problem, without configuring a Python module
    and CSS file. For more information, see
    :ref:`opencoursestaff:changing_visual_style_of_drag_and_drop_problem`.

To customize the style of drag and drop problems, follow these steps.

#. Create a custom CSS style sheet that applies styles to the drag and drop
   problem user interface. You can base your style sheet on the `example CSS
   file for drag and drop problems`_ that is included in the drag and drop
   problem module.

#. Create a Python module that includes your custom CSS style sheet. For
   example, the following Python module files include a CSS style sheet.

    .. code-block:: shell

        ./my_drag_and_drop_style
        ./my_drag_and_drop_style/css
        ./my_drag_and_drop_style/css/my_drag_and_drop_style.css
        ./my_drag_and_drop_style/__init__.py
        ./setup.py

   For information about creating and installing Python modules, see the
   documentation for the Python programming language.

#. Install your Python module on the LMS server as the ``edxapp`` user.

   .. code-block:: shell

        pip install /path/to/my/module


#. Edit the ``lms.env.json`` file for your LMS server. Add the ``drag-and-
   drop-v2`` object to the ``XBLOCK_SETTINGS`` object. Include the content
   shown in the following example.

   .. code-block:: json

           "XBLOCK_SETTINGS":{
                "drag-and-drop-v2": {
                    "theme": {
                        "package": "my_drag_and_drop_style",
                        "locations": ["css/my_drag_and_drop_style.css"]
                    }
                }

   Include the name of your Python module in the ``package`` object. Include
   the path to your CSS style sheet file in the ``locations`` object. The path
   must be relative to your Python module installation directory. You can
   include more than one path in the ``locations`` array, separated by commas.

#. Restart the LMS.

.. include:: ../../../../links/links.rst
