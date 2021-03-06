# Changelog

## Ginjo-Rfm 2.0.2

* Added configuration parameter ignore_bad_data to silence data mismatch errors when loading resultset into records.

* Added method to load a resultset from file or string. Rfm::Resultset.load_data(file_or_string).

* Added more specs for the above features and for the XmlParser module.

## Ginjo-Rfm 2.0.1

* Fixed bug in Base.find where options weren't being passed to Layout#find correctly.

* Fixed bug in rfm.rb when calling #models or #modelize.

## Ginjo-Rfm 2.0.0

* ActiveModel compatibility allows Rails ActiveRecord-style models.

* Alternative XML parsers using ActiveSupport::XmlMini interface.

* Compound queries with multiple omitable find-requests.

* Configuration API manages settings of multiple server/db/layout/etc setups.

* Full Filemaker metadata support.

## Ginjo-Rfm 1.4.4

* Fixed bug when creating empty value list.

* Additional fixes for Rfm::VERSION.

* Fixed Record getter/setter issue.

* Other minor fixes and cleanup.

* Added tests to rspec.

* Documentation cleanup.

## Ginjo-Rfm 1.4.3

* Fixed version management issue. Rfm::VERSION now works.

## Ginjo-Rfm 1.4.2

* Re-implemented:  
  
	Layout#field_controls

	Layout#value_lists  
  
* Enhanced:  

	ValueListItem handles both display & data items now.

	Timeout feature from timting (github/timting/rfm).

	Added specs for Record#save.  
  
* Fixed:  

	[Bug] Getting & setting fields with symbol-based keys was producing error.

	[Bug] Setting fields would not update main record hash.

	[Bug] Record#save wasn't merging back into self.  

* Partial Fix:  

	server.db.all
	db.layout.all
	db.script.all  
  
	Note: the "#all" method returns object names (as keys) only. The receiver of the method maintains the full object collection.  

	Example:  
  
	    server.db.all #=> ['dbname1', 'dbname2', ...]
	    server.db     #=> a DbFactory object (descendant of Hash), containing 0 or more Database objects

## Lardawge-Rfm 1.4.2 (unreleased)
  
* Made nil default on fields with no value.  
  
	Example:
 
	    Old: record.john #=> "" 
	    New: record.john #=> nil
   
## Lardawge-Rfm 1.4.1.2

* [Bug] Pointing out why testing is soooooo important when refactoring... Found a bug in getter/setter method in Rfm::Record (yes, added spec for it).

## Lardawge-Rfm 1.4.1.1

* [Bug] Inadvertently left out an attr_reader for server from resultset effecting container urls.

## Lardawge-Rfm 1.4.1*

* Changed Server#do_action to Server#connect.

* XML Parsing is now done via xpath which significantly speeds up parsing.

* Changes to accessor method names for Resultset#portals Resultset#fields to Resultset#portal_meta and Resultset#field_meta to better describe what you get back.

* Added an option to load portal records which defaults to false. This significantly speeds up load time when portals are present on the layout.

	Example:  
  
	    result = fm_server('layout').find({:username => "==#{username}"}, {:include_portals => true})
	    # => This will fetch all records with portal records attached.
  
	    result.first.portals
	    # => would return an empty hash by default.
    
* Internal file restructuring. Some classes have changed but it should be nothing a developer would use API wise. Please let me know if it is.

* Removed Layout#value_lists && Layout#field_controls. Will put back in if the demand is high. Needs a major refactor and different placement if it goes back in. Was broken so it didn't seem to be used by many devs.