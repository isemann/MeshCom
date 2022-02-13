# MeshCom 
is a tactical mesh-network for messaging and telemetry data using LoRa transceiver modules. There is no hierarchy in a mesh network topology, every node can relay a packet and cooperate with other nodes to efficiently route a packet to the gateways. Mesh networks dynamically connect end-nodes together and self-configure the routing paths.

<p align="center"><img src="images/meshcom_1.gif" alt="Meshcom Network"></p>

The Meshcom network is self-configured using flooding algorithms. In flood-based networking a node broadcasts a beacon message. The neighbouring nodes receive the message and relay it with a reception history. When the flooding process ends, most of the end-nodes would have received the beacon message several times either directly from a gateway or through other end-nodes. Thereafter, a mesh table is availaable in each end-node and in the gateways based on the reception history and received signal strength indication (RSSI) of the beacon message.

Following are the characteristics of the MeshCom network:
<ul>
<li>There is no need for cell-planning with the gateways, and the end-nodes can be deployed in a relatively simple and flexible manner.</li>

<li>The routing paths are established automatically among the end-nodes. If there is a failure in the existing routing path, re-routing is done in the network, and new paths are reconfigured.</li>

  <li>The network is optimized for low-rate communication at sub-GHz bands.</li>

  <li>N:1 and 1:N bidirectional communications are possible.</li>

  <li>The network is suitable for messaging, telentric data and ad-hoc communication</li>
</ul>

# Meshtastic Source-Code modified for MeshCom - licensed Radio Amateurs only (!):
* Bluetooth PIN set permanent to "000000" for MeshCom firmware, simplify operation for Radio Amateurs, no option to switch between 'licensed and non-licensed'.\
filename: nimble/BluetoothUtil.cpp, line 242\
    filename: src/DebugConfiguration.h, line 61
* HOP_Limit for sending reliable messages increased to 5, allowing messages to be relayed 5 times by nodes in the mesh network.\
filename: mesh/MeshTypes.h, line 37
* MeshCom logo and OEVSV link added to source\
filename: src/graphics/img/icon-meshcom.xbm\
rename icon.xbm --> icon-meshtastic\
filename: src/graphics/Screen.cpp, line 126
* Disable both sleep modi (light sleep, deep sleep), to keep devices permanently on without using the swtich 'always_on' to avoid hyperactivity of node\
filename: src/sleep.cpp
* Wifi Refresh reduced to 5sec\
filename: mesh/http/WifiAPClient.cpp, line 93
* Reconnect to MeshCom server after reboot\
filename: src/mqtt/MQTT.cpp
* ShortName = Suffix of Austrian Radio Amateur callsign, character 4-6, defaults to 'HAM' if callsign is shorter\
filename: scr/plugins/AdminPlugin.cpp, line 141-152, line 19
* Presettings for Meshcom:\
PSK Encryption NONE\
Channel: Very Long Range Very Slow (BW125kHz)\
Region: EU433\
filename: src/mesh/channles.cpp, line 94\
filename: src/configuration.h\
* Meshpacket size increase to 256\
filename: scr/mqtt/MQTT.cpp, line 189
* NTP source changed to MeshCom infrastructure\
filename: src/mesh/http/WiFiClient.cpp, line 26-27
* GPS position broadcast period increased to 15min for standard mode (no change to smart mode)\
filename: src/plugins\PositionPlugin.cpp, line 132-144
* QO-100 test link: borrow lorawan region setting "TW" for QRG 441.500 MHz to use qith TX Patrol (setting band start to 441.100 MHz for region TW --> default channel 2 = 441.500 MHz)\
filename: src/mesh/RadioInterface.cpp, line 26-27
* Mofification of position info parameters, send till channel utilization 100%
filename: src/plugins/PostionPlugin.cpp, line 139-176\



