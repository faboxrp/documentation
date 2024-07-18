=========
Accidents
=========

When managing a fleet of vehicles, eventually, accidents will occur. It is important to track these
occurrences to gain insights, from seeing which vehicles cost the most to keep on the road, to which
drivers have been in the most accidents.

Due to the customizable nature of Odoo's *Fleet* app, there are several different ways to track
accidents. The instructions below provides step by step instructions for only *one* method to keep
track of accidents and their subsequent repair costs.

Structure
=========

For this example, in order to track accidents, two service types are created: `Accident - Driver's
Fault` and `Accident - No Fault`.

This will make it possible to track the various repairs associated with accidents, organized by the
cause of the accident (who's fault the accident was).

Every time an accident occurs, a service record is created. The specific repairs needed for the
accident are logged in the *description* of the service record, and the details about the accident
(what happened) are logged in the *notes* section.

With this organization structure, it is possible to view all accidents organized by fault, car,
driver, and cost.

.. seealso::
   To manage accidents, the creation of service records is **required**.

   Refer to the :doc:`service` documentation for detailed instructions on how to create service
   records in Odoo's *Fleet* app.

Log an accident and repairs
===========================

After an accident occurs, repairs are needed. To log an accident, the first step is to :ref:`create
a service record <fleet/service-form>` detailing the specific repairs needed.

Navigate to :menuselection:`Fleet app --> Fleet --> Services` to vie the main :guilabel:`Services`
dashboard. Click :guilabel:`New` in the top-left corner and a service form loads.

Enter the following information on the form:

- :guilabel:`Description`: enter the description of repairs needed to fully repair the vehicle, such
  as `Bodywork`, `Windshield Replacement`, or `Replacement Bumper, Tires, and Windows`.
- :guilabel:`Service Type`: select either `Accident - Driver's Fault` or `Accident - No Fault`,
  depending on the situation.

  When entering either of these two :guilabel:`Service Types` for the first time, enter the
  new service type, then click :guilabel:`Create (new service type)`.

  Once an accident service type has been added, it is available from the drop-down menu in the
  :guilabel:`Service Type` field.
- :guilabel:`Date`: using the calendar popover window, select the date the accident occurred.
  Navigate to the desired month using the :icon:`fa-chevron-left` :icon:`fa-chevron-right`
  :guilabel:`(chevron)` icons, then click on the date to select it.
- :guilabel:`Cost`: leave this field *blank*, as the cost is not yet known.
- :guilabel:`Vendor`: select the vendor to perform the repairs using the drop-down menu. If the
  vendor has not already been entered in the system, type in the vendor name, and click either
  :guilabel:`Create` to add them, or :guilabel:`Create and edit...` to :ref:`add and configure the
  vendor <fleet/new-vendor>`.
- :guilabel:`Vehicle`: select the vehicle that was damaged in the accident from the drop-down menu.
  When the vehicle is selected, the :guilabel:`Driver` field is populated, and the unit of measure
  for the :guilabel:`Odometer Value` field appears.
- :guilabel:`Driver`: the current driver listed for the selected vehicle is populated when the
  :guilabel:`Vehicle` is selected. If a different driver was operating the vehicle when the accident
  occurred, select the correct driver from the drop-down menu.
- :guilabel:`Odometer Value`: enter the odometer reading when the accident occurred. The units of
  measure are either in kilometers (:guilabel:`km`) or miles (:guilabel:`mi`), depending on how the
  selected vehicle was configured.
- :guilabel:`NOTES`: enter the specific details for the accident at the bottom of the service form,
  such as `Hit a deer` or `Rear ended at an intersection while stopped`.

.. image:: accidents/service-form.png
   :align: center
   :alt: Enter the information for an accident repair.

.. note::
   Some accidents require multiple repairs with several different vendors (repair shops). For these
   scenarios, a separate service record is needed for each vendor performing the repairs. To keep
   records organized, it is recommended to keep the :guilabel:`NOTES` field identical.

Service stages
==============

In Odoo's *Fleet* app, there are four default service stages:

.. tabs::

   .. tab:: New

      The default stage when a service record is created. The service has been requested, but
      repairs have not begun. The cost field for this stage should be zero.

   .. tab:: Running

      The repair is in-process but not yet complete. The estimate for repairs should be listed in
      the cost field.

   .. tab:: Completed

      All repairs listed in the service form have been completed. The cost should be updated to
      reflect the final total cost charged for the repairs.

   .. tab:: Cancelled

      The service request has been canceled. Some common scenarios for this is when the estimate
      is higher than the remaining vehicle value, and is deemed not worth repairing.

During the repair process, change the service status to reflect the vehicle's current status.

Change the status in one of two ways: on the :ref:`individual service record
<fleet/service_record>`, or in the :ref:`Kanban service view <fleet/Kanban>`.

.. _fleet/service_record:

Service record
~~~~~~~~~~~~~~

Open the main :guilabel:`Services` dashboard by navigating to :menuselection:`Fleet app --> Fleet
--> Services`. Next, click on the individual service record to open the detailed service form. Click
the desired stage in the top-right corner above the service form to change the status.

.. image:: accidents/running.png
   :align: center
   :alt: The stages as seen from the service form.

.. _fleet/Kanban:

Kanban view
~~~~~~~~~~~

Open the main :guilabel:`Services` dashboard by navigating to :menuselection:`Fleet app --> Fleet
--> Services`. Remove the default :guilabel:`Service Type` filter in the :guilabel:`Search...` bar,
then click the :icon:`oi-view-kanban` :guilabel:`Kanban` icon in the top-right of the screen.

All services are organized by their respective :guilabel:`Status`. Drag-and-drop a service record to
the desired stage.

.. image:: accidents/drag-n-drop.png
   :align: center
   :alt: The Kanban view of stages, with a card being dragged and dropped to the Running stage.

Accident reporting
==================

One of the main reasons to track accidents using the method outlined in this document is the ability
to quickly view the amount of accidents, as well as determine the safest drivers. Multiple ways are
available to view service data, both from the main :guilabel:`Services` dashboard, or from the
:guilabel:`Reporting` dashboard.

Services dashboard
==================

On the default :guilabel:`Services` dashboard, all service records are grouped by :guilabel:`Service
Type`, in alphabetical order. The two service types created for accident tracking appear in the
list: :guilabel:`Accident - Driver Fault` and :guilabel:`Accident - No Fault`.

Each grouping displays the number of records within each grouping, and lists the individual records
beneath each grouping title.

.. example::
   In this example, there are six accidents where the driver was at fault, and four accidents that
   were not the driver's fault. This default dashboard also displays the estimated total
   :guilabel:`Cost` for all the accident in each group.

   There is an estimated `$19,164.81` dollars for driver-caused accident repairs, and an estimated
   `$2,548.21` dollars for no-fault accidents.

   .. image:: accidents/group-accidents.png
      :align: center
      :alt: alt text

.. note::
   The total :guilabel:`Cost` calculates **all** costs on the repair form, including estimated costs
   as well as final repair costs. This number may not be accurate if there are any repairs in the
   :guilabel:`Running` stage, and the final bill has not been calculated.

Managing accident repairs
-------------------------

For companies with multiple employees managing a large fleet of vehicles, displaying only services
in the :guilabel:`Running` stage can be itme-saving.

Navigate to the main :guilabel:`Services` dashboard, where all service requests are organized by
:guilabel:`Service Type`. Next, click the :icon:`fa-caret-down` :guilabel:`(down caret)` icon at the
far-right of the :guilabel:`Search...` bar, revealing a drop-down menu.
