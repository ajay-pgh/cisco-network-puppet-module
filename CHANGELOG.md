# Change Log
All notable changes to this project will be documented in this file.
This project adheres to [Semantic Versioning](http://semver.org/).

## [2.1.0] - 2019-08-19

### Added

### Changed
* Added performance enhancement to `cisco_interface` to improve processing time with small numbers of managed interfaces.

### Removed
- Removal of deprecated `cisco_interface` 'private-vlan' properties.

| Deprecated/Removed Name | New Name |
|:---|:---:|
| `private_vlan_mapping`                          | `pvlan_mapping`
| `switchport_mode_private_vlan_host`             | `switchport_pvlan_host`, `switchport_pvlan_promiscuous`,
| `switchport_mode_private_vlan_host_association` | `switchport_pvlan_host_association`
| `switchport_mode_private_vlan_host_promiscous`  | `switchport_pvlan_mapping`
| `switchport_mode_private_vlan_trunk_promiscuous`| `switchport_pvlan_trunk_promiscuous`
| `switchport_mode_private_vlan_trunk_secondary`  | `switchport_pvlan_trunk_secondary`
| `switchport_private_vlan_association_trunk`     | `switchport_pvlan_trunk_association`
| `switchport_private_vlan_mapping_trunk`         | `switchport_pvlan_mapping_trunk`
| `switchport_private_vlan_trunk_allowed_vlan`    | `switchport_pvlan_trunk_allowed_vlan`
| `switchport_private_vlan_trunk_native_vlan`     | `switchport_pvlan_trunk_native_vlan`

- Removal of deprecated `cisco_vlan` 'private-vlan' properties.

| Deprecated/Removed Name | New Name |
|:---|:---:|
| `private_vlan_association` | `pvlan_association`
| `private_vlan_type`        | `pvlan_type`

- Removed cisco_interface attribute:
   * `purge_config`

### Issues Addressed

- [Very slow execution when managing interfaces #496](https://github.com/cisco/cisco-network-puppet-module/issues/496)

## [2.0.1] - 2019-06-24

### Changed
* Module updated to utilize a transport class rather than the current device class.  Backwards compatible change.

## [2.0.0] - 2019-02-14

### New Major Version

This is a new major version release of the cisco-network-puppet-module.  This version of the module extends Cisco and Netdev resources to allow managing Cisco Nexus devices using an agentless workflow.

The traditional agent based workflows are still supported with the following caveats.

* GuestShell Agent
   * Supported on all platforms that have GuestShell support
   * Supports agent installs using puppet agent 5 and puppet agent 6 rpms.
* Native Bash Agent
   * Only supported on NX-OS image versions prior to release version `9.2(1)`
   * Supports agent installs using puppet agent 5 rpm only and support will be discontinued once puppet agent 5 reaches EOL.
* Open Agent Container (OAC)
   * This version of the module is not supported for OAC.  Must use module version `1.10.0` or ealier.
   * Supports agent install using puppet agent 4 rpm or ealier which is now EOL.

### Added
* Extended `cisco_ospf_vrf` with attribute:
   * `redistribute`
* Extended `cisco_vpc_domain` with attributes:
   * `arp_synchronize`
   * `nd_synchronize`
   * `peer_switch`
* Extended `cisco_vxlan_vtep_vni` with attribute:
   * `suppress_arp_disable`
* Extended `cisco_vxlan_vtep` with attributes:
   * `global_suppress_arp`
   * `global_mcast_group_l2`
   * `global_mcast_group_l3`
   * `global_ingress_replication_bgp`

### Changed

### Removed

### Resolved Issues

## [1.10.0] - 2018-09-19

**NOTE:** Starting in release `9.2(1)` and onward, installing the Puppet Agent into the `bash-shell` hosting environment is no longer supported.

The puppet agent software must be installed on a Cisco Nexus platform in the `Guestshell` (the Linux container environment running CentOS). This provides a secure, open execution environment that is decoupled from the host.

### New feature support

### Added
* Added `syslog_facility` with attribute:
   * `level`
* Extend syslog_server with attribute:
   * `facility`
* Extend cisco_interface with attribute:
   * `ipv6_redirects`
* Extend network_dns with attribute:
   * `hostname`

* Extend syslog_settings with attributes:
   * `logfile_name`
   * `logfile_severity_level`
   * `logfile_size`

*note: due to bug in NXAPI logfile_size is only supported on n9k and n3k platforms running `7.0(3)I7.4` / `9.2(1)` or higher*

* Added `banner` with attributes:
  * `motd`

*note: due to bug in NXAPI multiline banners are only supported on n9k and n3k platforms running `7.0(3)I7.4` / `9.2(1)` or higher*

### Changed

### Removed
* Support for Puppet Agent install into the `bash-shell` hosting environment. This is the native WRL Linux environment underlying NX-OS.

### Resolved Issues
* https://tickets.puppetlabs.com/browse/CISCO-63
* https://tickets.puppetlabs.com/browse/CISCO-66
* https://tickets.puppetlabs.com/browse/CISCO-71
* https://tickets.puppetlabs.com/browse/CISCO-72
* https://tickets.puppetlabs.com/browse/CISCO-73
* https://tickets.puppetlabs.com/browse/CISCO-74
* https://tickets.puppetlabs.com/browse/CISCO-75
* https://tickets.puppetlabs.com/browse/CISCO-76
* https://tickets.puppetlabs.com/browse/CISCO-77

## [1.9.0] - 2018-04-19

### New feature support
#### Cisco Resources
- `cisco_evpn_multisite` type and provider.
- `cisco_evpn_stormcontrol` type and provider.
- `cisco_interface_evpn_multisite` type and provider.
- `cisco_evpn_multicast` type and provider.
- `cisco_ip_multicast` type and provider

### Added
- Extend `cisco_bgp_neighbor` with attribute:
  - `peer_type`
- Extend `cisco_bgp_neighbor_af` with attribute:
  - `rewrite_evpn_rt_asn`
- Extend `cisco_vxlan_vtep` with attribute:
  - `multisite_border_gateway_interface`
- Extend `cisco_vxlan_vtep_vni` with attribute:
  - `multisite_ingress_replication`
- Extend `cisco_vrf_af` with attributes:
  - `route_target_both_auto_mvpn`
  - `route_target_import_mvpn`
  - `route_target_export_mvpn`

### Changed

### Removed

### Resolved Issues

## [1.8.0] - 2017-12-12

### New feature support
#### Cisco Resources
- `cisco_object_group` type and provider.
- `cisco_object_group_entry` type and provider.

### Added

### Changed
- `cisco_interface` Refactored to allow physical ethernet interfaces to be managed as ensurable resources.
  - `ensure => absent` for physical interfaces will put the interface into a default state.
  - `ensure => absent` for logical interfaces will cause them to be destroyed.

- Extend `syslog_server` with attribute:
 - `port`

- Extend `syslog_settings` with attributes:
 - `console`
 - `monitor`
 - `source_interface`
 - `vrf`

- Extend `radius_global` with attribute:
 - `source_interface`

- Extend `tacacs_global` with attribute:
 - `source_interface`

### Removed

### Resolved Issues

## [1.7.0] - 2017-05-31

### New feature support
#### Cisco Resources
- `cisco_bgp_af_aa` type and provider.

### Added
- Extend cisco_interface with attributes:
 - `purge_config`

- Extend cisco_interface_channel_group with attributes:
 - `channel_group_mode`

- Added support for tftp and usb URIs to `cisco_upgrade`

- Extend `cisco_upgrade` with attributes:
 - `package`

- Added `ntp_auth_key` with attributes:
 - `algorithm`
 - `key`
 - `mode`
 - `password`

- Extend `ntp_config` with attributes:
 - `authenticate`
 - `trusted_key`

- Extend `ntp_server` with attributes:
 - `key`
 - `maxpoll`
 - `minpoll`
 - `vrf`

### Changed

### Removed
- Deprecated `version` and `source_uri` attributes for `cisco_upgrade` in favor of a single attribute `package`.

### Resolved Issues
* https://github.com/cisco/cisco-network-puppet-module/issues/424
* https://github.com/cisco/cisco-network-puppet-module/issues/432
* https://github.com/cisco/cisco-network-puppet-module/issues/446
* https://github.com/cisco/cisco-network-puppet-module/issues/452

## [1.6.0] - 2017-03-13

### New feature support
#### Cisco Resources
- `cisco_route_map` type and provider.
- `cisco_upgrade` type and provider.

### Added
- Extend cisco_interface with attributes:
 - `load_interval_counter_1_delay`
 - `load_interval_counter_2_delay`
 - `load_interval_counter_3_delay`

### Changed

### Removed

### Resolved Issues
* https://github.com/cisco/cisco-network-puppet-module/issues/413
* https://github.com/cisco/cisco-network-puppet-module/issues/414
* https://github.com/cisco/cisco-network-puppet-module/issues/415
* https://github.com/cisco/cisco-network-puppet-module/issues/417
* https://github.com/cisco/cisco-network-puppet-module/issues/419
* https://github.com/cisco/cisco-network-puppet-module/issues/420
* https://github.com/cisco/cisco-network-puppet-module/issues/423

## [1.5.0] - 2017-01-11

### New feature support
#### Cisco Resources
- `cisco_hsrp_global` type and provider.
- `cisco_interface_hsrp_group` type and provider.

### Added
- Extend cisco_interface with attributes:
 - `hsrp_bfd`
 - `hsrp_delay_minimum`
 - `hsrp_delay_reload`
 - `hsrp_mac_refresh`
 - `hsrp_use_bia`
 - `hsrp_version`
 - `pim_bfd`

- Extend cisco_pim with attributes:
 - `bfd`

* Added support for Cisco NX-OS software releases `7.3(0)F1(1)` and `8.0(1)`

### Resolved Issues
* https://github.com/cisco/cisco-network-puppet-module/issues/408

## [1.4.1] - 2016-11-02

### Added
- Extend cisco_bgp with attributes:
 - `event_history_errors`
 - `event_history_objstore`
- Added support for Cisco NX-OS software release `7.3(0)I5(1)`

### Changed

### Removed

## [1.4.0] - 2016-10-04

### New feature support
#### Cisco Resources
- `cisco_bfd_global` type and provider.
- `cisco_dhcp_relay_global` type and provider.
- `cisco_ospf_area` type and provider.
- `cisco_ospf_area_vlink` type and provider.

### Added
- Extend cisco_interface with attributes:
 - `bfd_echo`
 - `ipv4_dhcp_relay_addr`
 - `ipv4_dhcp_relay_info_trust`
 - `ipv4_dhcp_relay_src_addr_hsrp`
 - `ipv4_dhcp_relay_src_intf`
 - `ipv4_dhcp_relay_subnet_broadcast`
 - `ipv4_dhcp_smart_relay`
 - `ipv6_dhcp_relay_addr`
 - `ipv6_dhcp_relay_src_intf`
 - `storm_control_broadcast`
 - `storm_control_multicast`
 - `storm_control_unicast`
- Extend cisco_interface_ospf with attributes:
 - `bfd`
 - `mtu_ignore`
 - `network_type`
 - `priority`
 - `shutdown`
 - `transmit_delay`
- Extend cisco_interface_portchannel with attributes:
 - `bfd_per_link`
- Extend cisco_ospf_vrf with attributes:
 - `bfd`
- Extend cisco_bgp_neighbor with attributes:
 - `bfd`
- Extended `cisco_bgp_af` to include l2vpn/evpn address-family support

- Deprecated `cisco_interface` 'private-vlan' properties and replaced with new methods. The deprecated properties will be removed with release 2.0.0. The old -> new properties are:

| Old Name | New Name(s) |
|:---|:---:|
| `private_vlan_mapping`                          | `pvlan_mapping`
| `switchport_mode_private_vlan_host`             | `switchport_pvlan_host`, `switchport_pvlan_promiscuous`,
| `switchport_mode_private_vlan_host_association` | `switchport_pvlan_host_association`
| `switchport_mode_private_vlan_host_promiscous`  | `switchport_pvlan_mapping`
| `switchport_mode_private_vlan_trunk_promiscuous`| `switchport_pvlan_trunk_promiscuous`
| `switchport_mode_private_vlan_trunk_secondary`  | `switchport_pvlan_trunk_secondary`
| `switchport_private_vlan_association_trunk`     | `switchport_pvlan_trunk_association`
| `switchport_private_vlan_mapping_trunk`         | `switchport_pvlan_mapping_trunk`
| `switchport_private_vlan_trunk_allowed_vlan`    | `switchport_pvlan_trunk_allowed_vlan`
| `switchport_private_vlan_trunk_native_vlan`     | `switchport_pvlan_trunk_native_vlan`

- Deprecated `cisco_vlan` 'private-vlan' properties and replaced with new methods. The deprecated properties will be removed with release 2.0.0. The old -> new properties are:

| Old Name | New Name |
|:---|:---:|
| `private_vlan_association` | `pvlan_association`
| `private_vlan_type`        | `pvlan_type`

### Changed
- `cisco_interface_ospf` type and provider so that the properties accept 'default' keyword.

## [1.3.2] - 2016-07-26
### Fixed:
- Remove `autorequire` references in cisco types.
  - Fixes incompatibility between cisco resources and latest puppet agent rpm.
- Fix `undefined method 'previous'` bug in `cisco_command_config` provider.

## [1.3.1] - 2016-05-06

### New feature support
#### Cisco Resources
- `cisco_fabricpath_global` type and provider.
- `cisco_fabricpath_topology` type and provider.
- `cisco_itd_device_group` type and provider.
- `cisco_itd_device_group_node` type and provider.
- `cisco_itd_service` type and provider.
- `cisco_stp_global` type and provider.

### Added
- Extended the following providers to support `Nexus N5k`, `Nexus N6k`, and `Nexus N7k`
  - `cisco_aaa_authentication_login`, `cisco_aaa_authorization_login_cfg_svc`, `cisco_aaa_authorization_login_exec_svc`, `cisco_aaa_group_tacacs`
  - `cisco_fabricpath_global`, `cisco_fabricpath_topology`
  - `cisco_interface_channel_group`, `cisco_interface_portchannel`, `cisco_portchannel_global`
  - `cisco_snmp_community`, `cisco_snmp_group`, `cisco_snmp_server`, `cisco_snmp_user`
  - `cisco_vpc_domain`
  - `cisco_vtp`
  - `domain_name`, `name_server`, `network_dns`, `network_vlan`, `search_domain`
  - `ntp_config`, `ntp_server`
  - `port_channel`
  - `radius`, `radius_global`, `radius_server`, `radius_server_group`
  - `network_snmp`, `snmp_community`, `snmp_notification`, `snmp_notification_receiver`, `snmp_user`
  - `tacacs`, `tacacs_global`, `tacacs_server`, `tacacs_server_group`
- Extended `cisco_bgp` with the following attributes:
  - `nsr`
  - `reconnect_interval`
- Extended `cisco_interface` with the following attributes:
  - `ipv4_forwarding`, `switchport_mode fabricpath`
  - `stp_bpdufilter`, `stp_bpduguard`, `stp_cost`, `stp_guard`, `stp_link_type`, `stp_mst_cost`
  - `stp_mst_port_priority`, `stp_port_priority`, `stp_port_type`, `stp_vlan_cost`, `stp_vlan_port_priority`
  - `switchport_mode_private_vlan_host`, `switchport_mode_private_vlan_host_association`
  - `switchport_mode_private_vlan_host_promisc`, `switchport_mode_private_vlan_trunk_promiscuous`
  - `switchport_mode_private_vlan_trunk_secondary`, `switchport_private_vlan_association_trunk`
  - `switchport_private_vlan_mapping_trunk`, `switchport_private_vlan_trunk_allowed_vlan`
  - `switchport_private_vlan_trunk_native_vlan`, `private_vlan_mapping`
  - `modify switchport_trunk_allowed_vlan to use range_summarize() which takes care of idempotency issues with vlan ranges`
- Extended `cisco_portchannel_global` provider to support `Nexus N3k`
- Extended `cisco_vlan` with the following attributes:
  - `mode`
  - `private_vlan_type`
  - `private_vlan_association`
- Extended `cisco_vpc_domain` with the following attributes:
  - `fabricpath_emulated_switch_id`
  - `fabricpath_multicast_load_balance`
  - `port_channel_limit`
- Extended `cisco_vrf_af` with the following attributes:
  - `route_policy_export`
  - `route_policy_import`
  - `route_target_export_stitching`
  - `route_target_import_stitching`
- Extended `cisco_vxlan_vtep` with the following attributes:
  - `source_interface_hold_down_time`

### Removed
- Removed 'cisco_nxapi' fact as this gem is no longer a dependency.

### Changed
- Renamed all providers from `:nxapi` to `:cisco` as they may include support for multiple Cisco platforms, not all of which use NXAPI.

## 1.3.0
This version was never released.

## [1.2.3] - 2016-02-24
### Added
- Download link for Nexus 5000 and Nexus 6000 Open Agent Container (OAC).
- OAC programmability guide links.
- Complete cisco_ace documentation.

## [1.2.2] - 2016-02-14

### Fixed
- Fixed Cisco NetDev port\_channel provider to use the correct cisco\_node\_utils object.
- Fixed beaker test setup and cleanup issues.
- Fixed incomplete documentation references for the open agent container (OAC)

## 1.2.1
This version was never released.

## [1.2.0] - 2016-02-12

### New feature support
#### Cisco Resources
- `cisco_aaa_authentication_login` type and provider.
- `cisco_aaa_authorization_login_cfg_svc` type and provider.
- `cisco_aaa_authorization_login_exec_svc` type and provider.
- `cisco_aaa_group_tacacs` type and provider.
- `cisco_ace` type and provider
- `cisco_acl` type and provider
- `cisco_evpn_vni` type and provider.
- `cisco_interface_channel_group` type and provider
- `cisco_interface_portchannel` type and provider
- `cisco_interface_service_vni` type and provider
- `cisco_overlay_global` type and provider.
- `cisco_pim` type and provider
- `cisco_pim_rp_address` type and provider
- `cisco_pim_grouplist` type and provider
- `cisco_portchannel_global` type and provider
- `cisco_vdc` type and provider.
- `cisco_vpc_domain` type and provider.
- `cisco_vni` type and provider.
- `cisco_vrf_af` type and provider.
- `cisco_vxlan_vtep` type and provider.

#### NetDev Resources
- `network_trunk` provider.
- `port_channel` provider.
- `search_domain` provider.
- `snmp_notification` provider.

### Added
- Extended `cisco_bgp` with the following attributes:
  - `disable_policy_batching`, `disable_policy_batching_ipv4`, `disable_policy_batching_ipv6`
  - `fast_external_fallover`
  - `flush_routes`
  - `isolate`
  - `neighbor_down_fib_accelerate`
  - `route_distinguisher`
  - `event_history_cli`
  - `event_history_detail`
  - `event_history_events`
  - `event_history_periodic`
- Extended `cisco_bgp_af` with the following attributes:
  - `default_metric`
  - `distance_ebgp`, `distance_ibgp`, `distance_local`
  - `inject_map`
  - `table_map`, `table_map_filter`
  - `suppress_inactive`
- Extended `cisco_interface` with the following attributes:
  - `fabric_forwarding_anycast_gateway`
  - `ipv4_address_secondary`, `ipv4_netmask_length_secondary`
  - `ipv4_arp_timeout`
  - `ipv4_pim_sparse_mode`
  - `vlan_mapping`, `vlan_mapping_enable`
  - `ipv4_acl_in`, `ipv4_acl_out`, `ipv6_acl_in`, `ipv6_acl_out`
  - `vpc_id`, `vpc_peer_link`
- Extended `cisco_vrf` with the following attributes:
  - `route_distinguisher`
  - `vni`

### Removed

## [1.1.0] - 2015-11-02

### New feature support
#### Cisco Resources.
- cisco_bgp type and provider.
- cisco_bgp_af type and provider.
- cisco_bgp_neighbor type and provider.
- cisco_bgp_neighbor_af type and provider.
- cisco_vrf type and provider.

#### NetDev Resources.
- domain_name provider.
- name_server provider.
- network_dns provider.
- network_snmp provider.
- ntp_config provider.
- ntp_server provider.
- radius provider.
- radius global provider.
- snmp_notification_receiver provider.
- snmp_user provider.
- syslog_server provider.
- syslog_setting provider.

### Added
- New documentation for developing beaker testcases: README-develop-beaker-scripts.md
- Extended cisco_interface with the following attributes:
  - encapsulation dot1q
  - mtu
  - speed
  - duplex
  - switchport trunk allowed VLANs
  - switchport trunk native VLAN
- Added support for network_interface from puppets netdev_stdlib
- Rubocop enabled and passes (@robert-w-gries)
- Gemfile now requires puppet version 4.0 or higher
- Gemfile.lock added to gitignore

### Removed
- Obsolete documents: README-beaker-testcase-execution.md, README-beaker-testcase-writing.md
- Travis no longer tests ruby version 1.9.3

## [1.0.2] - 2015-09-28
### Fixed
- Updated documentation links to reflect that the repo and agent RPM packages have had their platform renamed from 'nxos' to 'cisco-wrlinux'.

## [1.0.1] - 2015-09-18
### Fixed
- Fixed broken documentation links

## [1.0.0] - 2015-08-28
### Added
- New facts `cisco_node_utils` and `cisco_nxapi` report the installed version of these gems.
- Providers requiring the `cisco_node_utils` feature will generate a warning message if an obsolete gem version is installed.
- Added README-maintainers.md

### Fixed
- Metadata URLs now point to new public GitHub repository.
- Moved misc READMEs into /docs
- NXAPI providers are marked as defaultfor 'nexus' operating system.
- Fixed beaker test for package and interface ospf
- Fixed sample install.pp

## [0.9.1] - 2015-08-13
### Added
- Added CONTRIBUTING.md
- Added README-creating-types-providers.md and associated templates.
- Added SUPPORT.md
- Added Beaker test cases for cisco_command_config, file, package, and service providers.
- Added VRF attribute to cisco_interface provider.

### Fixed
- 'puppet resource cisco_vtp' now works properly.
- cisco_interface, cisco_ospf_vrf, and cisco_vlan now properly handle destroy/recreate scenarios.
- Added missing methods in cisco_ospf_vrf provider.
- Style cleanup of many Beaker test scripts.
- Fixed title pattern error in 'puppet resource cisco_snmp_group'.
- Avoid inadvertently suppressing relevant exceptions.
- Added dotted-decimal munging for area in cisco_interface_ospf
- Modified template placeholder names to meet lint reqs

## 0.9.0 - 2015-07-24
### Added
- Initial release of puppetlabs-ciscopuppet module, supporting Cisco NX-OS software release 7.0(3)I2(1) on Cisco Nexus switch platforms: N95xx, N93xx, N30xx and N31xx.
- Please note: 0.9.0 is an EFT pre-release for a limited audience with access to NX-OS 7.0(3)I2(1). Additional code changes may occur in 0.9.x prior to the final 1.0.0 release.

[2.1.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v2.0.1...v2.1.0
[2.0.1]: https://github.com/cisco/cisco-network-puppet-module/compare/v2.0.0...v2.0.1
[2.0.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.10.0...v2.0.0
[1.10.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.9.0...v1.10.0
[1.9.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.8.0...v1.9.0
[1.8.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.7.0...v1.8.0
[1.7.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.6.0...v1.7.0
[1.6.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.5.0...v1.6.0
[1.5.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.4.1...v1.5.0
[1.4.1]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.4.0...v1.4.1
[1.4.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.3.2...v1.4.0
[1.3.2]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.3.1...v1.3.2
[1.3.1]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.2.3...v1.3.1
[1.2.3]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.2.2...v1.2.3
[1.2.2]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.2.0...v1.2.2
[1.2.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.0.2...v1.1.0
[1.0.2]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/cisco/cisco-network-puppet-module/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/cisco/cisco-network-puppet-module/compare/v0.9.1...v1.0.0
[0.9.1]: https://github.com/cisco/cisco-network-puppet-module/compare/v0.9.0...v0.9.1
