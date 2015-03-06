=== Intercom for WordPress ===
Contributors: lumpysimon
Donate link: http://lumpylemon.co.uk
Tags: intercom, intercom.io, crm, messaging, contact form, support, email, feedback, customer relationship management, users
Requires at least: 3.8
Tested up to: 4.1
Stable tag: trunk

Easy integration of the Intercom CRM and messaging app into your WordPress website.

== Description ==

[Intercom](http://intercom.io) is a customer relationship management (CRM) and messaging tool for web app owners. WordPress is being widely used as a web app nowadays, so Intercom is an ideal companion app to find out more about your users, contact them, get their instant feedback, and track your relationship with them over time so you can spot those who need attention.

This plugin generates the Javascript install code to integrate all of this functionality into your WordPress-powered web app.

You can also optionally send extra custom data (attributes) about your users, as well as company data.

== Frequently Asked Questions ==

= What on earth is Intercom and what is a CRM? =

Take a look at http://intercom.io, they explain it better than I can!

= Does this plugin track all visitors to my site? =

No, it only tracks logged-in users. The administrator is not tracked.

= How do I exclude other user roles from being tracked? =

Simply add the `hide_from_intercom` capability to the user role.

The following example will exclude editors, you should put this code in your theme's functions.php or a plugin:

`
$role = get_role( 'editor' );
$role->add_cap( 'hide_from_intercom' );
`

= Can I choose the format of the username sent to Intercom? =

Yes, you can choose between "Firstname Lastname" or the user's displayname.

= Can I send custom user attributes? =

Yes, on the options screen you can choose to send the user's role and/or website URL.

= Can I add my own custom user attributes? =

Yes, there is a filter called `ll_intercom_custom_data` that you can use to filter the `$custom` array. For each extra custom user attribute you wish to send, you should add a key => value array element (e.g. `Age => 42` ).

Here's an example that sends the user's age based on the value in a usermeta field. This code should be placed in your theme's functions.php file or in a plugin:

`
add_filter( 'll_intercom_custom_data', 'my_intercom_data' );

function my_intercom_data( $custom ) {

	$user_id = get_current_user_id();

	if ( $age = get_user_meta( $user_id, 'age', true ) ) {
		$custom['Age'] = $age ;
	}

	return $custom;

}
`

Make sure you read Intercom's [custom user attributes documentation](http://docs.intercom.io/configuring-Intercom/Send-custom-user-attributes-to-Intercom).

= Can I send company data? =

Yes, you can add this using the `ll_intercom_company_data` filter. Your function should return the company data as an array. Here's a simple example:

`
add_filter( 'll_intercom_company_data', 'my_intercom_company_data' );

function my_intercom_company_data() {

	$company = array(
		'id'         => 100,
		'name'       => 'My Cool Company',
		'created_at' => strtotime( '10 June 2011' )
		);

	return $company;

}
`

Please read Intercom's [company data documentation](http://docs.intercom.io/configuring-Intercom/grouping-users-by-company).

= Can I use my own activator link instead of the default Intercom one? =

This plugin uses Intercom's default 'activator', but you can use your own one via the `ll_intercom_activator` filter.

Here's an example that uses all links with the `my-activator` class:

`
add_filter( 'll_intercom_activator', 'my_intercom_activator' );

function my_intercom_activator( $activator ) {

	return '.my-activator';

}
`

= Are Intercom and this plugin secure? =

It is highly recommended to enable Intercom's "secure mode". All communications between your website and Intercom will then use a secret key to generate a 'hash' with every request - this prevents users maliciously sending messages as another user. Please read Intercom's [secure mode documentation](http://docs.intercom.io/configuring-Intercom/enable-secure-mode).

= Does this plugin work on older versions of WordPress or PHP? =

Possibly, but I've not tried. I can only provide support if you're using the latest version of this plugin together with the latest version of WordPress and PHP 5.2.4 or newer.

== Installation ==

1. Upload the intercom-for-wordpress folder to your wp-content/plugins/ directory.
2. Activate the plugin through the Plugins menu in WordPress.
3. Go to the settings page.
4. Enter your Intercom App ID.
6. Choose your preferred username format, optional custom data and whether to track admin pages.
7. Highly recommended: for extra security, enable secure mode from within your Intercom app and enter your secret key in the settings page.

== Changelog ==

= 1.0 (6th November 2104) =
* Improve the custom activator code so it doesn't override the 'Display messenger button' setting in Intercom

= 0.9 (30th September 2104) =
* Add ll_intercom_company_data filter so plugins/themes can send company data
* Update install code

= 0.8 (23rd January 2104) =
* Make secure mode optional
* Update installation instructions and FAQ

= 0.7 (September 2013) =
* Use json_encode for generating the install code (thanks to [John Blackbourn](http://profiles.wordpress.org/johnbillion))
* Send user ID by default and remove from settings screen
* Add ll_intercom_activator filter so plugins/themes can use their own link ID/class

= 0.6 (July 2013) =
* Make the secret key field mandatory and do not output the install code if it is not set
* Remove redundant code that was generating a PHP notice
* Tested for compatibility with WordPress 3.6

= 0.5 (June 2013) =
* Add option to allow tracking of admin pages (off by default)
* Update install code to load JavaScript from CDN

= 0.4 (April 2013) =
* Use latest version of the install code
* Add filter (ll_intercom_custom_data) so plugins/themes can add their own custom data

= 0.3.1 (January 2013) =
* Fix Multisite network-activated options saving bug
* Remove default options

= 0.3 (January 2013) =
* Fix kses missing arguments bug
* Multisite-compatible options page
* Use latest version of the install code
* Remove the label option (no longer supported by Intercom)
* Various code improvements and DocBlock comments

= 0.2 (January 2012) =
* Corrected user capability check when displaying reminder notice
* Added description and code comments
* Added 'Like this Plugin?' section to settings screen
* Code tidy-up

= 0.1 (January 2012) =
* Initial release
