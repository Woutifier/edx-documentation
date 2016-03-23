.. _Create Coupons:

########################
Creating Coupon Codes
########################

.. This feature is not in Dogwood.

You can use coupon codes to provide discounted or free course enrollments to
your learners. Two types of coupon codes are available.

* Discount code: These codes offer a discount of up to 99% off the cost of a
  course.
* Enrollment code: These codes offer a 100% discount off the cost of a course.

Both discount codes and enrollment codes can be used in the following ways.

* One time by one user.
* One time by multiple users.
* Multiple times by multiple users.

When you create a coupon code, the E-Commerce service generates an order. The
Invoice Payment Processor module records these orders and assumes out-of-band
payment for the coupon codes.

The Invoice Payment Processor module records the transaction in the Invoice
table for later reconciliation.

****************************
Create Coupon Codes
****************************

You create coupon codes by using the coupon administration tool, which is
located at ``http://localhost:8002/coupons/``.

#. In your browser, go to ``http://localhost:8002/coupons/`` to open the coupon
   administration tool, and then select **Create Coupon**.
#. On the **Create New Coupon** page, enter the following information.

   .. note::
     All of the following fields are required. After you create a coupon code,
     you can only change the **Valid from** and **Valid until** dates.

   * **Name**: The name you want to give the coupon, such as "Holiday 2015 15%
     Promotion". The name must have fewer than 255 characters.
   * **Course ID**: The ID of the course that you want to provide the coupon
     for. The course ID is <how does the user know the course ID?>.
   * **Code Type**: Select either **Discount Code** or **Enrollment Code**. For
     more information, see :ref:`Create Coupons`.
   * **Seat Type**: The type of "seat" in the course. For example, this may be
     "verified" or "professional". The options for this field appear after you
     enter a valid value in the **Course ID** field.
   * **Category**: Suggested categories for your coupon code. These categories
     can help you keep track of your codes.

     .. Coming soon (per 3/23 meeting): **Notes**: Any notes that you want to
     .. include about the coupon code, such as why it was created.

   * **Valid from** and **Valid until**: The dates and times when you want to
     start and stop offering the coupon code, respectively. The time zone is
     set to Universal Coordinated Time (UTC). You can edit these fields after
     you create the coupon.
   * **Discount Value**: This field is only visible if you select **Discount
     Code** for **Code Type**. Enter the percent or U.S. dollar amount discount
     that you want to offer, then select **Percent** or **Fixed**.

#. (Optional) On the **Create New Coupon** page, enter the following
   information. All of these fields are optional.

   * **Usage Limitations**: The way your coupon code can be used. Options are
     **Can be used once by one customer**, **Can be used once by multiple
     customers**, or **Can be used multiple times by multiple customers**.
   * **Number of codes**: This field is visible if you select **Can be used
     once by one customer**. This value specifies the number of individual
     codes you want to create. Make sure that you create enough codes so that
     each person receives one code.
   * **Code**: This field is visible if you select **Can be used once by
     multiple customers** or **Can be used multiple times by multiple
     customers**.

     * If you select **Can be used once by multiple customers**, leave this
       field empty. The system generates the code for you when you select
       **Create Coupon**.

     * If you select **Can be used multiple times by multiple customers**, you
       can either enter a value in this field or leave it empty.  <You can
       enter alphanumeric characters as well as underscores.> For example, you
       can enter ``HOLIDAY_15``. If you leave this field empty, the system
       generates a code for you.

       .. Are these options currently available on Open edX?
       .. What generates the redeem code email? - Has to be done manually by whoever creates/distributes enrollment codes.

   * **Client**: The name of the organization that you create the codes for.
     This organization receives an invoice for the codes you create.
   * **Total Paid**: The amount that will be invoiced to the client.

#. Select **Create Coupon**.

When you select **Create Coupon**, a page for your coupon opens. This page
lists the information for your coupon code, including any individual codes that
the system generated as well as the URLs where users can redeem the coupon
codes. To download a .csv file that lists all of this information, select
**Download**.


****************************
Edit Coupon Codes
****************************

You edit coupon codes by using the coupon administration tool.

.. note::
 You can only edit the **Valid from** and **Valid until** information.

#. In your browser, go to ``http://localhost:8002/coupons/`` to open the coupon
   administration tool.
#. On the **Coupon Codes** page, locate the coupon that you want in the table,
   and then select the name of the coupon.
#. On the page for the coupon, select **Edit Coupon**.

   If the coupon has been edited before, the username of the person who last
   edited the coupon is visible, along with the date and time of the last edit.

#. In the **Valid from** or **Valid until** field, enter the date and time that
   you want.
#. Select **Save Changes**.

.. _Download Coupon Code Information:

***********************************
Download Coupon Code Information
***********************************

After you create a coupon code, you can download a .csv file that lists
information such as the name of the coupon code, the URL where a user can
redeem the coupon code, the status of the coupon code, and the user who created
the coupon code. If your coupon code includes multiple individual codes, the
.csv lists information for all of the codes associated with your coupon code.

#. In your browser, go to ``http://localhost:8002/coupons/`` to open the coupon
   administration tool.
#. On the **Coupon Codes** page, locate the coupon that you want in the table,
   and then select the name of the coupon.
#. On the page for the coupon, select **Download**. Your .csv file begins
   downloading automatically.
#. Open the .csv file that you downloaded.


***************************************
Enable Learners to Redeem Coupon Codes
***************************************

Learners redeem coupon codes in two ways.

* By entering a coupon code on the **Checkout** page for the verified or
  professional certificate track. In this case, you provide the coupon code for
  the learner to enter.

* By visiting a URL. At this URL, the enrollment code or discount code is
  applied automatically, and the learner is enrolled in the course if they
  haven't already enrolled. In this case, you provide the URL for the learner
  to visit.

==================================================
Learners Enter a Coupon Code on the Checkout Page
==================================================

When learners enter a coupon code on the **Checkout** page, you provide the learners with the coupon codes that they will enter.



=======================
Learners Visit a URL
=======================


You can download a .csv file that includes all of the codes for an individual coupon, as well as the URLs where learners can redeem the codes.

After you create coupon codes, you can download a .csv file that includes all
the individual coupon codes as well as URLs where the learner can redeem the codes.
The E-Commerce service provides two ways for learners to use these URLs to
redeem coupon codes.

(You provide these to learners in the form of URL)

* The offer landing page URL.

  When a learner clicks an offer landing page URL...
  The offer landing page is a web page
  The offer landing page presents the offer to the learner and confirms that
  entering the coupon code enrolls the learner in the course. Learners do not
  have to register or sign in to go to the offer landing page. However,
  learners do have to register or sign in when they redeem the code and enroll
  in the course.

* A redeem endpoint URL.

  When a learner

  Using a redeem endpoint takes the learner to a web page

  adds the course that is associated with the coupon code
  to the learner's basket, applies the coupon code, and completes the order and
  course enrollment. This endpoint requires registration or sign-in. After the
  order is complete, the learner's dashboard opens, and the course the learner
  just enrolled in is visible.

.. note::
  If the coupon code is a discount code, and the learner has a balance due
  after the learner arrives at the offer landing page or the redeem endpoint,
  the checkout page opens after the learner applies the discount code.


Offer Landing Page
*************************

The offer landing page presents the offer to the learner and confirms that
entering the coupon code enrolls the learner in the course. Learners do not
have to register or sign in to go to the offer landing page. However,
learners do have to register or sign in when they redeem the code and enroll
in the course.

To direct learners to the offer landing page, send them a URL for the coupon
code that uses the following format.

``http://localhost:8002/coupons/offer/?code=<code number>``

For example, an offer landing page URL might resemble the following example.

``http://localhost:8002/coupons/offer/?code=ZDPC3AQV3732RQT5``

Redeem Endpoint
********************

The redeem endpoint adds the course that is associated with the coupon code
to the learner's basket, applies the coupon code, and completes the order and
course enrollment. This endpoint requires registration or sign-in. After the
order is complete, the learner's dashboard opens, and the course the learner
just enrolled in is visible.

To direct learners to the redeem endpoint, send them a URL for the coupon
code that uses the following format.

``http://localhost:8002/coupons/redeem/?code=<code number>``

For example, a redeem endpoint URL might resemble the following example.

``http://localhost:8002/coupons/redeem/?code=ZDPC3AQV3732RQT5``

.. note::
 In the .csv file, all URLs are formatted as
 ``http://localhost:8002/coupons/offer/?code=<code number>``. To direct the
 learner to a URL that includes a redeem endpoint, change ``offer`` in the
 URL to ``redeem``.


************************
Example Email Messages
************************





=======================
Enter a Coupon Code
=======================

.. code::

 Dear <name>,

 You have received a <discount/enrollment> code for <course name>. For more
 information about the course, see <course About page>.

 To redeem this code, sign up for the <verified/professional> certificate
 track, and then enter the following code in the **Coupon Code** field on the
 **Checkout** page:

 ``ZDPC3AQV3732RQT5``

 We look forward to learning with you!

 The <course name> course team


=======================
Learners Visit a URL
=======================

Offer Landing Page
*************************

.. code::

 Dear <name>,

 You have received a <discount/enrollment> code for <name of course>. To redeem
 this code and enroll in the course, select the following link:

``http://localhost:8002/coupons/redeem/?code=ZDPC3AQV3732RQT5``


Redeem Endpoint
********************

.. code::

 Dear <name>,

 You have received a <discount/enrollment> code for <name of course>. To redeem
 this code and enroll in the course, select the following link:

``http://localhost:8002/coupons/offer/?code=ZDPC3AQV3732RQT5``
