# GlideTime Online Billing
GTO (GlideTime Online) has a powerful billing subsystem designed to handle the majority of our clubs flight billing needs,  reporting itemized flight billing to both pilots and our accountant.

# Billing Tags
Each flight has a set of billing tags stored with it.  These tags describe the flight for the billing system.  The flight tags combine information about both the flight and the pilots.  These tags and the flight details (eg times) are what drives the billing system.  See below for same example tags.

Each time a flight is changed these tags are regenerated and stored.  So, for example, if the wrong pilot was accidentally selected for a flight, not a problem, fixing the pilot will update the tags as needed and all previous costings will automatically update.

The flight tags represent the state of the flight at the time and do not change once a flight has been invoiced.  So, for example,  if a pilot changes from Youth to Senior, previous flights will remain tagged (and thus billed) as Youth.  This helps maintain a correct historical record of charges.  A pilot can look at their old flights and still see the bill items applied.
 
Some example billing tags and their meanings.

- **NOCHARGE** No charge for this flight
- **INSTR** Instructional flight
- **CROSS** Cross country flight
- **FCFS** Fix cost flying scheme
- **SIX_OK** One of the first 6 flights for Six Flight scheme
- **MQSYND** MQ syndicate member
- **SCOUT** Scout group
- **1ST** First flight of the day for this pilot
- **SELF** Self launch
- **WINCH** Winch launch
- **AEROTOW** : Aerotow launch

# Billing Rules files
The server contains dated rules files that describe the pricing that apply from that date forward.  If prices change then a new dated rules file is needed.

These files are kept in the **gto/app/Billing** folder in git.  New files are applied by committing updated rules file(s) to git then updating the gto server.

The rules files contain descriptions of billable line items along with the gliders, airfields and tags they apply to.  For example some of the line items in the current billing rules are **Glider [OR/PR] per/min**, **Glider [PB] per/min**, **Winch fee**, **Landing fee**, **Landing fee (self launch)**.

Each line item has rules describing the flight tags that match and a cost for one of the following categories **glider_per_minute**, **towplane_per_minute**, **fixed charge**.

# Monthly Accounting Report
At the end of the month the treasurer will run the accounting report.  This validates all unbilled flights, generates a .csv file for the accounting package then tags each flight with the billing date.  Once a flight has been tagged as billed it is locked and only Admin can edit it.

# Nightly Email Script
Every night, after flying, a script scans the database and emails pilots with a summary of their day's flights and costs.  It also notifies pilots of missing data on their flights.  e.g. no landing time. 

# Special Event Pricing
 To handle special event pricing for a day (eg half price gliders, family day). You need to create two new billing files with appropriate dates.  One to start the new pricing.  The second to reactivate the original pricing.

 These can be placed on the server any time before billing, although I would recommend adding them before the event itself.  You can optionally use the **SPECIAL** tag which is activated by checking the **Event Pricing** flight page checkbox.  That tag allows a combination of special and normal pricing on the same day.
