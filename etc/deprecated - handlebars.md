This code selectable mode from main.handlebars is deprecated in favor of reload-settings route linked from admin ("Advanced") section
```html
			{{#groupContains "admin" @root.user.username}}
			<li class="nav-item"><p class="navbar-text"><a href="{{get_proxy_prefix_then_slash}}admin/?section={{@root.section}}&mode=reload-settings">Reload Settings</a>
			{{!--
			<form class="form-inline" action="{{get_proxy_prefix_then_slash}}admin" method="post">
				<input type="hidden" name="mode" id="mode" value="reload-settings"/>
				<button class="btn btn-default">Reload Settings</button>
			</form>
			--}}
			</p>
			</li>
			{{/groupContains}}

```


This code is deprecated (user_selectable_modes instead which excludes transient modes and modes available for user if were in another section)
```xml
			{{#each modes_by_section}}
				{{#if_eq @key @root.section}}
					<table>
					<tr>
					{{#each this}}
					<td>
					<form action="{{get_proxy_prefix_then_slash}}">
					<input type="hidden" name="section" id="section" value="{{@root.section}}"/>
					<input type="hidden" name="mode" id="mode" value="{{this}}" />
					{{#if_eq this @root.mode}}
					<input class="btn" type="submit" value="{{friendlyModeName this}}" />
					{{else}}
					<input class="btn btn-default" type="submit" value="{{friendlyModeName this}}" />
					{{/if_eq}}
					</form>
					</td>
					{{/each}}
					</tr>
					</table>
				{{/if_eq}}
			{{/each}}
```

This code is deprecated (use link instead):
```xml
			{{!--
			<form action="{{get_proxy_prefix_then_slash}}">
			<input type="hidden" name="section" id="section" value="{{this}}"/>
			{{#if_eq this @root.section}}
				<input class="btn btn-link disabled" type="submit" value="{{friendlySectionName this}}" />
			{{else}}
				<input class="btn btn-link" type="submit" value="{{friendlySectionName this}}" />
			{{/if_eq}}
			</form>--}}
```

This code is deprecated (instead, use compact link area in heading for choices and invisible table for content):
```xml
	<div class="panel panel-default">
		<div class="panel-heading">
			<div class="panel-title pull-right">
				<table>
				<tr>
			{{#each user_selectable_modes}}
				<td>
				<form action="{{get_proxy_prefix_then_slash}}">
				<input type="hidden" name="section" id="section" value="{{@root.section}}"/>
				<input type="hidden" name="mode" id="mode" value="{{this}}" />
				{{#if_eq this @root.mode}}
				<input class="btn" type="submit" value="{{friendlyModeName this}}" />
				{{else}}
				<input class="btn btn-default" type="submit" value="{{friendlyModeName this}}" />
				{{/if_eq}}
				</form>
				</td>
			{{/each}}
				</tr>
				</table>
			
			</div>
			<div class="clearfix"></div> {{!--fills out height of the title row, so float doesn't cause text to hang out the bottom--}}
		</div>
		<div class="panel-body">
		</div>
	</div>
```	

```xml
    {{#if_eq mode "create"}}
	{{#createGroupContains "care" user.username}}
	<form class="form-horizontal" id="student-microevent" action="{{get_proxy_prefix_then_slash}}student-microevent" method="post">
		<input type="hidden" name="section" value="{{section}}"/>
		{{#if_blank prefill_mode}}
		<input type="hidden" name="mode" id="mode" value="create"/>
		{{else}}
		<input type="hidden" name="mode" id="mode" value="{{prefill_mode}}"/>
		{{/if_blank}}
		
		<div class="form-group">
			<label class="control-label col-sm-2" >Student First Name:</label>
			<div class="col-sm-10">
				<input class="form-control" type="text" name="first_name" value="{{prefill_first_name}}"/>
			</div>
		</div>
		<div class="form-group">
			<label class="control-label col-sm-2" >Student Last Name:</label>
			<div class="col-sm-10">
				<input class="form-control" type="text" name="last_name" value="{{prefill_last_name}}"/>
			</div>
		</div>
		<div class="form-group">
			<label class="control-label col-sm-2" >Grade:</label>
			<div class="col-sm-10">
				<input class="form-control" type="text" name="grade_level" value="{{prefill_grade_level}}"/>
			</div>
		</div>
		<div class="form-group">
			<label class="control-label col-sm-2" >Pickup/Dropoff by:</label>
			<div class="col-sm-10">
				<input class="form-control" type="text" name="chaperone" value="{{prefill_chaperone}}"/>
			</div>
		</div>

		<div class="form-group">
			<label class="control-label col-sm-2" style="color:darkgray">Time (blank for auto, else include AM/PM):</label>
			<div class="col-sm-10">
				<input class="form-control" type="text" name="stated_time" value="{{prefill_stated_time}}"/>
			</div>
		</div>
		<div class="form-group">
			<label class="control-label col-sm-2" style="color:darkgray">Date (blank for auto, else include MM/DD/YYYY):</label>
			<div class="col-sm-10">
				<input class="form-control" type="text" name="stated_date" value="{{prefill_stated_date}}"/>
			</div>
		</div>
		<div class="form-group">
			<label class="control-label col-sm-2" style="color:darkgray">Family ID (if applicable):</label>
			<div class="col-sm-10">
				<input class="form-control" type="text" name="family_id" value="{{prefill_family_id}}"/>
			</div>
		</div>
		<div class="form-group">
			<div class="col-sm-10" style="text-align:center">
				<input type="submit" class="btn btn-primary btn-sm" value="Enter"/>
			</div>
		</div>			
	<div class="form-group">
	{{#is_after_school}}
	<div class="col-sm-10" style="text-align:center" style="font-style:italic;">Sign student out</div>
	{{else}}
	<div class="col-sm-10" style="text-align:center" style="font-style:italic;">Sign student in</div>
	{{/is_after_school}}
	</div>
		<span style="color:darkgray">{{show_time}}</span>
	</form>
	
	{{/createGroupContains}}
	{{#createGroupContains "commute" user.username}}
	<!--<h1>Student Commute</h1>-->
	<form class="form-horizontal" id="student-microevent" action="{{get_proxy_prefix_then_slash}}student-microevent" method="post">
		<input type="hidden" name="section" value="commute"/>
		{{!--#if_eq prefill_mode ""--}}
		{{#if_blank prefill_mode}}
		<input type="hidden" name="mode" id="mode" value="create"/>
		{{else}}
		<input type="hidden" name="mode" id="mode" value="{{prefill_mode}}"/>
		{{/if_blank}}
		<div class="form-group">
			<label class="control-label col-sm-2" >Student Name:</label>
			<div class="col-sm-10">
				<input class="form-control" type="text" name="name" value="{{prefill_name}}"/>
			</div>
			<label class="control-label col-sm-2" > &nbsp;Grade:</label>
			<div class="col-sm-10">
				<input class="form-control" type="text" name="grade_level" value="{{prefill_grade_level}}"/>
			</div>
		</div>
		<div class="form-group">
			<label class="control-label col-sm-2" >Heading:</label>
			<div class="col-sm-10">
				<div class="btn-group" data-toggle="buttons">
					<label class="btn btn-primary"><input type="radio" name="heading" value="in"/>in</label>
					<label class="btn btn-primary"><input type="radio" name="heading" value="out"/>out</label>
				</div>
			</div>
		</div>
		<div class="form-group">
			<label class="control-label col-sm-2" >Reason:</label>
			<div class="col-sm-10">
				<input class="form-control" type="text" name="reason" value="{{prefill_reason}}"/>
			</div>
		</div>
		<div class="form-group">
			<div class="col-sm-10" style="text-align:center">
				<input type="submit" class="btn btn-primary btn-sm" value="Enter"/>
				<a data-toggle="collapse" href="#custom-time" class="btn btn-default btn-md" role="button">More Options</a>
			</div>
		</div>
		{{#user_has_pinless_time section user.username}}
		<div name="custom-time" id="custom-time">
		{{else}}
		<div name="custom-time" class="collapse" id="custom-time">
		{{/user_has_pinless_time}}
			<div style="text-align:center; color:darkgray">{{show_time}}
			</div>
			<div class="form-group">
				<label class="control-label col-sm-2" style="color:darkgray">Custom Time:</label>
				<div class="col-sm-10">
					<input class="form-control" type="text" name="stated_time" value="{{prefill_stated_time}}"/>
				</div>
			</div>
			<div class="form-group">
				<label class="control-label col-sm-2" style="color:darkgray">Date (blank for auto, else include MM/DD/YYYY):</label>
				<div class="col-sm-10">
					<input class="form-control" type="text" name="stated_date" value="{{prefill_stated_date}}"/>
				</div>
			</div>
			{{#user_has_pinless_time section user.username}}
			<!--(pinless entry)-->
			{{else}}
			<div class="form-group">
				<label class="control-label col-sm-2" style="color:darkgray">override pin:</label>
				<div class="col-sm-10">
					<input class="form-control" type="password" name="pin" value=""/>
				</div>
			</div>
			{{/user_has_pinless_time}}
		</div>
	</form>
	{{/createGroupContains}}

	{{/if_eq}}
```


This code is deprecated by show_history helper
```xml
<table class="table table-hover" style="width:100%">
		<thead class="thead-default">
		<tr>
			<td style="width:10em">&nbsp;</td>{{!--Edit button column--}}
			{{!--#each this_sheet_field_friendly_names}}
			<td style="width:10em">{{this}}</td>
			{{/each--}}

			{{!--Column headers--}}
			{{#eachProperty objects.[0]}}
			<th>{{property}}&nbsp;</th>
			{{/eachProperty}}

			{{!--
			<td style="width:8em">&nbsp;</td>
			<td style="width:8em">Time</td>
			<td style="">Name<br></td>
			<td style="width:3em">Grade<br/>Level</td>
			<td style="width:20em">Reason</td>--}}
		</tr>
		</thead>
		<tbody>
		{{#each objects as |entryValue entryKey|}}
		<tr>
			<td>
			<form action="{{get_proxy_prefix_then_slash}}">
			<input type="hidden" name="section" id="section" value="{{@root.section}}"/>
			<input type="hidden" name="mode" id="mode" value="create"/>{{!--always use create form for editing--}}
			<input type="hidden" name="prefill_mode" id="prefill_mode" value="modify"/>{{!--always prefill modify for Edit button--}}
			<input type="hidden" name="prefill_name" id="prefill_name" value="{{this.name}}"/>
			<input type="hidden" name="prefill_year" id="prefill_year" value="{{@root.selected_year}}" />
			<input type="hidden" name="prefill_month" id="prefill_month" value="{{@root.selected_month}}" />
			<input type="hidden" name="prefill_day" id="prefill_day" value="{{@root.selected_day}}" />
			<input type="hidden" name="prefill_key" id="prefill_key" value="{{key}}" />
			{{!--<input class="btn btn-default" type="submit" value="Edit" />--}}
			</form>

			</td>
			{{!--#each @root.this_sheet_field_names as |fieldValue fieldKey|}}
				{{#if_formula this}}
				<td>&nbsp; </td>
				{{else}}
				<td>{{entryValue}}.{{fieldValue}}</td>
				{{/if_formula}}
			{{/each--}}
			{{#eachProperty this}}
			<td> {{value}}</td>
			{{/eachProperty }}
			{{!--
			<td>{{heading}}</td>
			<td>{{time}} </td>
			<td>{{name}}</td>
			<td>{{grade_level}}</td>
			<td>{{reason}}</td>--}}
		</tr>
		{{/each}}
		</tbody>
		</table>
```
