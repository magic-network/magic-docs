# Hardware Prerequisites

To be a magic wifi provider, you need the following devices:

1. Wifi Router (Access Point)
1. Gateway server device

## Wifi Router (Access Point)

Most Wifi-enabled routers can be re-purposed as Magic Access Points, as long as they have the following features:

- **WPA2-Enterprise**, which enables RADIUS, the open-source AAA(Authentication, Authorization, & Accounting) server which magic utilizes. 
- **RFC-5176 Support** - Change-of-Authorization & Disconnect messages.  Without this feature, Magic doesn't have the ability to disconnect people from your network.

It may be difficult to know if your router supports the above features. A router diagnostics 
tool will be provided soon to run against your router, but in the meantime, we recommend purchasing one of these inexpensive & fully-featured routers:

Recommended Routers:
- [MicroTik](https://mikrotik.com/products) ~$20

*in some cases, your router may have the features available, but your firmware doesn't support them.  In this case, you may use
the open source router firmware called [OpenWrt](https://openwrt.org/).*

## Gateway Server Device

This is a separate device, such as a Raspberry Pi, that runs the magic-agent in the "gateway" role.  All authentication
requests to use your magic router will be sent through this device, and it will be where you configure the availability and
pricing of your Access Point.

*Raspberry Pi device setup guide (coming soon)*

*We will soon support a cloud-based gateway server to reduce the need to run a local device for this role.*