<?php

class Alti_ProtectUploads
{

	protected $version;
	protected $plugin_name;
	protected $loader;

	public function __construct()
	{
		$this->version = '0.3';
		$this->plugin_name = 'protect-uploads';
		$this->load_dependencies();
		$this->set_locale();
		$this->define_admin_hooks();
	}

	private function load_dependencies()
	{

		require_once plugin_dir_path(dirname(__FILE__)) . 'includes/class-protect-uploads-loader.php';
		require_once plugin_dir_path(dirname(__FILE__)) . 'includes/class-protect-uploads-i18n.php';
		require_once plugin_dir_path(dirname(__FILE__)) . 'admin/class-protect-uploads-admin.php';

		$this->loader = new Alti_ProtectUploads_Loader();
	}

	/**
	 * set locale for translation ends.
	 */
	private function set_locale()
	{

		$plugin_i18n = new Alti_ProtectUploads_i18n();
		$plugin_i18n->set_domain($this->get_plugin_name());

		$this->loader->add_action('plugins_loaded', $plugin_i18n, 'load_plugin_textdomain');
	}

	/**
	 * action and filter for admin side
	 */
	private function define_admin_hooks()
	{

		$plugin_admin = new Alti_ProtectUploads_Admin($this->get_plugin_name(), $this->get_version());

		$this->loader->add_action('admin_menu', $plugin_admin, 'add_submenu_page');
		$this->loader->add_filter('plugin_action_links_' . $this->get_plugin_name() . '/' . $this->get_plugin_name() . '.php', $plugin_admin, 'add_settings_link');
		$this->loader->add_action('admin_enqueue_scripts', $plugin_admin, 'enqueue_styles');
	}

	public function run()
	{
		$this->loader->run();
	}

	public function get_plugin_name()
	{
		return $this->plugin_name;
	}

	public function get_loader()
	{
		return $this->loader;
	}

	public function get_version()
	{
		return $this->version;
	}
}
