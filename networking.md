[Back to Overview](https://github.com/BRO-FHV/docs/blob/master/README.md)
## <a name="Networking"></a>Networking

This Project uses LWIP for basic networking tasks. The porting is inspired by Starterware.

![LWIP Port](http://processors.wiki.ti.com/images/e/ec/StarterWare_Ethernet.jpg "Source: http://processors.wiki.ti.com/index.php/StarterWare_CPSW_Port_lwIP")

### Problems
In the basic lib we have some unaligned accesses. This was caused by unpacked structs in the porting part.

### Solution
The solution was to implement the IP/UDP part for our own. This was accomplished by define structs for each protokoll header and cast the data package.

Example: UDP header contains the IP and Ethernet header. This prevented the unaliged accesses.

```c
typedef struct {
	uint8_t destMacAddr[MAC_ADDR_LENGTH];
	uint8_t srcMacAddr[MAC_ADDR_LENGTH];
	uint8_t type[TYPE_LENGTH];
} eth_header_t;

typedef struct {
	uint8_t ethHeader[14];

	unsigned version :4;
	unsigned ihl :4;
	uint8_t tos;
	uint16_t tot_len;
	uint16_t ident;
	uint16_t flags_offset;
	uint8_t ttl;
	uint8_t protocol;
	uint16_t checksum;
	uint8_t srcIp[IP_ADDR_LENGTH];
	uint8_t destIp[IP_ADDR_LENGTH];
} ip_header_t;

typedef struct {
	uint8_t ethHeader[14];
	uint8_t ipHeader[20];

	uint8_t srcPort[2];
	uint8_t destPort[2];
	uint8_t len[2];
	uint8_t checksum[2];

	uint8_t data1;
	uint8_t data2;

	uint8_t dataRestStart;
} udp_header_t;
```

### Current State
In the current state it is possible to receive and send packages with UPD. An application can start listing for a specific port and can poll for incoming data.

### Outlook
For a real usage of LWIP it would be important to fix the Port and use the whole lib. That would raise the security and the reliability.

After that the IPC should be implemented to async inform the Application for incoming packages.

### Code Example

```c
void main() {
	BroUdpInit(PORT);

	while (1) {
		if (BroUdpHasData(PORT)) {
			printf("echo\n");

			upd_package_t* package = BroUdpGetData(PORT);
			BroUdpSendData(package->sender, PORT, package->data, package->len);

			free(package->data);
			package->data = NULL;
			package->len = 0;
		}
	}
}
```
