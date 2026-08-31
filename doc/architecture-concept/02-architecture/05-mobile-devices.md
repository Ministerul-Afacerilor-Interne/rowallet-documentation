# 2.5 Mobile Devices

This section defines the hardware and software requirements for mobile devices running the Wallet App.

<table>
  <thead>
    <tr>
      <th>Requirement</th>
      <th>Android</th>
      <th>iOS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Operating System Version</td>
      <td>Android 14, 15, 16 or 17</td>
      <td>iOS 18 or 26</td>
    </tr>
    <tr>
      <td>Android Security Patch Level /<br> iOS minor OS version</td>
      <td>t.b.d.</td>
      <td>t.b.d.</td>
    </tr>
    <tr>
      <td>Hardware-backed Key Store</td>
      <td>Required (TEE or StrongBox)</td>
      <td>Required (Secure Enclave)</td>
    </tr>
    <tr>
      <td>NFC</td>
      <td colspan="2" align="center">ISO 14443 A/B (for eID card reading)</td>
    </tr>
    <tr>
      <td>Internet Connection</td>
      <td colspan="2" align="center">Required</td>
    </tr>
    <tr>
      <td>Lock Screen</td>
      <td colspan="2" align="center">Required</td>
    </tr>
  </tbody>
</table>

The wallet solution only supports operating system versions that continue to receive regular security updates. For Android, this means versions that are still supported by the Android Open Source Project. As of July 2026, these are Android 14, 15, 16 and 17. For iOS, this includes versions that continue to receive general security updates from Apple, currently iOS 18 and iOS 26.

The minimum required security patch freshness has not yet been decided. On Android, this requirement will be based on the Android security patch level. On iOS, where no separate security patch level is exposed, it will instead be based on the installed iOS minor OS version.
