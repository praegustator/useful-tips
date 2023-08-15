## TLS handshake fails when traffic flows through WireGuard tunnel

On the client-side router ([documentation](https://help.mikrotik.com/docs/display/ROS/Mangle#Mangle-ChangeMSS), [source](https://forum.mikrotik.com/viewtopic.php?t=184115#p919168)):

```plaintext
/ip firewall/mangle/
  add out-interface=pppoe-out1
  protocol=tcp
  tcp-flags=syn
  action=change-mss
  new-mss=1360
  chain=forward
  tcp-mss=1301-65535
```
