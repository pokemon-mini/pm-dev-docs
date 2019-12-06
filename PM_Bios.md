## The BIOS Overview

The internal BIOS consists of a 4kB program image built to initialize
the system, bring it out of sleep and various other system specific
tasks. Since the Pokemon Mini is never technically off, only suspended,
BIOS is used for tasks like enabling power to the system and responding
to various at rest IRQs.

The BIOS image begins with a 256 byte IRQ vector table, consisting of
128 16-bit vectors (only first 76 are valid). The system reserves 32
vectors for hardware IRQs, the rest are used for software calls. It is
worth noting that all IRQs are latched on the rising edge of an event,
so button presses and IR receive is only latched when the IR receiver is
active 1 or if a button has been press, but not released.

## The IRQ Vector Table

<table>
<caption><strong>Bios IRQ Vector Table</strong></caption>
<thead>
<tr class="header">
<th><p>IRQ</p></th>
<th><p>BIOS</p></th>
<th><p>Cart IRQ</p></th>
<th><p>IRQ Group</p></th>
<th><p>Hardware Strobe</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>$00</p></td>
<td><p>0000:009A</p></td>
<td><p>0</p></td>
<td><p>Non-Maskable</p></td>
<td><p>System Start-up / System Reset</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>$01</p></td>
<td><p>0002:00AB</p></td>
<td></td>
<td><p>Non-Maskable</p></td>
<td><p>Unused</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$02</p></td>
<td><p>0004:00AB</p></td>
<td></td>
<td><p>Non-Maskable</p></td>
<td><p>Unused</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>$03</p></td>
<td><p>0006:01CF</p></td>
<td><p>1</p></td>
<td><p>$20[7..6]</p></td>
<td><p>$27,7</p></td>
<td><p><a href="PM_PRC" title="wikilink">PRC Copy Complete</a></p></td>
</tr>
<tr class="odd">
<td><p>$04</p></td>
<td><p>0008:01E0</p></td>
<td><p>2</p></td>
<td><p>$20[7..6]</p></td>
<td><p>$27,6</p></td>
<td><p><a href="PM_PRC" title="wikilink">PRC Frame Divider Overflow</a></p></td>
</tr>
<tr class="even">
<td><p>$05</p></td>
<td><p>000A:01F1</p></td>
<td><p>3</p></td>
<td><p>$20[5..4]</p></td>
<td><p>$27,5</p></td>
<td><p><a href="Timers" title="wikilink">Timer2 Upper-8 Underflow</a></p></td>
</tr>
<tr class="odd">
<td><p>$06</p></td>
<td><p>000C:0202</p></td>
<td><p>4</p></td>
<td><p>$20[5..4]</p></td>
<td><p>$27,4</p></td>
<td><p><a href="Timers" title="wikilink">Timer2 Lower-8 Underflow (8-bit only)</a></p></td>
</tr>
<tr class="even">
<td><p>$07</p></td>
<td><p>000E:0213</p></td>
<td><p>5</p></td>
<td><p>$20[3..2]</p></td>
<td><p>$27,3</p></td>
<td><p><a href="Timers" title="wikilink">Timer1 Upper-8 Underflow</a></p></td>
</tr>
<tr class="odd">
<td><p>$08</p></td>
<td><p>0010:0224</p></td>
<td><p>6</p></td>
<td><p>$20[3..2]</p></td>
<td><p>$27,2</p></td>
<td><p><a href="Timers" title="wikilink">Timer1 Lower-8 Underflow (8-bit only)</a></p></td>
</tr>
<tr class="even">
<td><p>$09</p></td>
<td><p>0012:0235</p></td>
<td><p>7</p></td>
<td><p>$20[1..0]</p></td>
<td><p>$27,1</p></td>
<td><p><a href="Timers" title="wikilink">Timer3 Upper-8 Underflow</a></p></td>
</tr>
<tr class="odd">
<td><p>$0A</p></td>
<td><p>0014:0246</p></td>
<td><p>8</p></td>
<td><p>$20[1..0]</p></td>
<td><p>$27,0</p></td>
<td><p><a href="Timers" title="wikilink">Timer3 Pivot</a></p></td>
</tr>
<tr class="even">
<td><p>$0B</p></td>
<td><p>0016:025A</p></td>
<td><p>9</p></td>
<td><p>$21[7..6]</p></td>
<td><p>$28,5</p></td>
<td><p>32Hz (From 256Hz Timer)</p></td>
</tr>
<tr class="odd">
<td><p>$0C</p></td>
<td><p>0018:026B</p></td>
<td><p>10</p></td>
<td><p>$21[7..6]</p></td>
<td><p>$28,4</p></td>
<td><p>8Hz (From 256Hz Timer)</p></td>
</tr>
<tr class="even">
<td><p>$0D</p></td>
<td><p>001A:027C</p></td>
<td><p>11</p></td>
<td><p>$21[7..6]</p></td>
<td><p>$28,3</p></td>
<td><p>2Hz (From 256Hz Timer)</p></td>
</tr>
<tr class="odd">
<td><p>$0E</p></td>
<td><p>001C:028D</p></td>
<td><p>12</p></td>
<td><p>$21[7..6]</p></td>
<td><p>$28,2</p></td>
<td><p>1Hz (From 256Hz Timer)</p></td>
</tr>
<tr class="even">
<td><p>$0F</p></td>
<td><p>001E:029E</p></td>
<td><p>13</p></td>
<td><p>$22[1..0]</p></td>
<td><p>$2A,7</p></td>
<td><p>IR Receiver</p></td>
</tr>
<tr class="odd">
<td><p>$10</p></td>
<td><p>0020:02AF</p></td>
<td><p>14</p></td>
<td><p>$22[1..0]</p></td>
<td><p>$2A,6</p></td>
<td><p>Shock Sensor</p></td>
</tr>
<tr class="even">
<td><p>$11</p></td>
<td><p>0022:00AB</p></td>
<td></td>
<td></td>
<td><p>$2A,5</p></td>
<td><p>Unused</p></td>
</tr>
<tr class="odd">
<td><p>$12</p></td>
<td><p>0024:00AB</p></td>
<td></td>
<td></td>
<td><p>$2A,4</p></td>
<td><p>Unused</p></td>
</tr>
<tr class="even">
<td><p>$13</p></td>
<td><p>0026:043E</p></td>
<td></td>
<td><p>$21[5..4]</p></td>
<td><p>$28,1</p></td>
<td><p>Cartridge Ejected</p></td>
</tr>
<tr class="odd">
<td><p>$14</p></td>
<td><p>0028:02C0</p></td>
<td><p>26</p></td>
<td><p>$21[5..4]</p></td>
<td><p>$28,0</p></td>
<td><p>Cartridge IRQ</p></td>
</tr>
<tr class="even">
<td><p>$15</p></td>
<td><p>002A:03BA</p></td>
<td><p>15</p></td>
<td><p>$21[3..2]</p></td>
<td><p>$29,7</p></td>
<td><p>Power Key</p></td>
</tr>
<tr class="odd">
<td><p>$16</p></td>
<td><p>002C:02D1</p></td>
<td><p>16</p></td>
<td><p>$21[3..2]</p></td>
<td><p>$29,6</p></td>
<td><p>Right Key</p></td>
</tr>
<tr class="even">
<td><p>$17</p></td>
<td><p>002E:02E2</p></td>
<td><p>17</p></td>
<td><p>$21[3..2]</p></td>
<td><p>$29,5</p></td>
<td><p>Left Key</p></td>
</tr>
<tr class="odd">
<td><p>$18</p></td>
<td><p>0030:02F3</p></td>
<td><p>18</p></td>
<td><p>$21[3..2]</p></td>
<td><p>$29,4</p></td>
<td><p>Down Key</p></td>
</tr>
<tr class="even">
<td><p>$19</p></td>
<td><p>0032:0304</p></td>
<td><p>19</p></td>
<td><p>$21[3..2]</p></td>
<td><p>$29,3</p></td>
<td><p>Up Key</p></td>
</tr>
<tr class="odd">
<td><p>$1A</p></td>
<td><p>0034:0315</p></td>
<td><p>20</p></td>
<td><p>$21[3..2]</p></td>
<td><p>$29,2</p></td>
<td><p>C Key</p></td>
</tr>
<tr class="even">
<td><p>$1B</p></td>
<td><p>0036:0326</p></td>
<td><p>21</p></td>
<td><p>$21[3..2]</p></td>
<td><p>$29,1</p></td>
<td><p>B Key</p></td>
</tr>
<tr class="odd">
<td><p>$1C</p></td>
<td><p>0038:0337</p></td>
<td><p>22</p></td>
<td><p>$21[3..2]</p></td>
<td><p>$29,0</p></td>
<td><p>A Key</p></td>
</tr>
<tr class="even">
<td><p>$1D</p></td>
<td><p>003A:0348</p></td>
<td><p>23</p></td>
<td></td>
<td><p>$2A,2</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$1E</p></td>
<td><p>003C:035C</p></td>
<td><p>24</p></td>
<td></td>
<td><p>$2A,1</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>$1F</p></td>
<td><p>003E:036D</p></td>
<td><p>25</p></td>
<td></td>
<td><p>$2A,0</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IRQ</p></td>
<td><p>BIOS</p></td>
<td><p>(Software only) Description</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$20</p></td>
<td><p>0040:FFF1</p></td>
<td><p>User IRQ Routine at PC 0xFFF1</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$21</p></td>
<td><p>0042:0713</p></td>
<td><p>Suspend System</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$22</p></td>
<td><p>0044:077C</p></td>
<td><p>Sleep ??</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$23</p></td>
<td><p>0046:078B</p></td>
<td><p>Sleep with display on ??</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$24</p></td>
<td><p>0048:079D</p></td>
<td><p>Shutdown System (Use this to exit your game!)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$25</p></td>
<td><p>004A:07B1</p></td>
<td><p>?? (Involves Cartridge Eject)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$26</p></td>
<td><p>004C:07E9</p></td>
<td><p>Set default LCD Constrast (A = Contrast level 0x00 to 0x3F)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$27</p></td>
<td><p>004E:0802</p></td>
<td><p>Increase or decrease Contrast based of Zero flag (0 = Increase, 1 = Decrease)<br />
Return A = 0x00 if succeed, 0xFF if not.</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$28</p></td>
<td><p>0050:081B</p></td>
<td><p>Apply default LCD Constrast</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$29</p></td>
<td><p>0052:0821</p></td>
<td><p>Get default LCD Contrast (return A)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$2A</p></td>
<td><p>0054:0830</p></td>
<td><p>Set temporary LCD Constrast (A = Contrast level 0x00 to 0x3F)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$2B</p></td>
<td><p>0056:084E</p></td>
<td><p>Turn LCD On</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$2C</p></td>
<td><p>0058:0871</p></td>
<td><p>Initialize LCD</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$2D</p></td>
<td><p>005A:08CB</p></td>
<td><p>Turn LCD Off</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$2E</p></td>
<td><p>005C:08EC</p></td>
<td><p>Enable RAM vector. (Check if Register 0x01 Bit 7 is set, if not, it set bit 6 and 7)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$2F</p></td>
<td><p>005E:0904</p></td>
<td><p>Disable RAM vector</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$30</p></td>
<td><p>0060:0923</p></td>
<td><p>Disable Cart Eject IRQ 13 (with abort)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$31</p></td>
<td><p>0062:092E</p></td>
<td><p>Enable Cart Eject IRQ 13 (with abort)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$32</p></td>
<td><p>0064:0949</p></td>
<td><p>?? (Involves Cartridge Eject)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$33</p></td>
<td><p>0066:0961</p></td>
<td><p>?? (Involves Cartridge Eject)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$34</p></td>
<td><p>0068:097D</p></td>
<td><p>Nintendo Dev Card (??)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$35</p></td>
<td><p>006A:09E4</p></td>
<td><p>Nintendo Dev Card (??)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$36</p></td>
<td><p>006C:0A4F</p></td>
<td><p>?? (Involves Cartridge Eject)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$37</p></td>
<td><p>006E:0A76</p></td>
<td><p>Disable Cartridge Eject IRQ (Reg 0x24, Bit 1 = 0)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$38</p></td>
<td><p>0070:0A81</p></td>
<td><p>?? (Involves Cartridge Eject)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$39</p></td>
<td><p>0072:0AA6</p></td>
<td><p>Rumored to speed up CPU?</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$3A</p></td>
<td><p>0074:0ACD</p></td>
<td><p>Recover from IRQ $39?</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$3B</p></td>
<td><p>0076:0AE6</p></td>
<td><p>Cart power off and update state</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$3C</p></td>
<td><p>0078:0AF9</p></td>
<td><p>Cart power on and update state</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$3D</p></td>
<td><p>007A:0B20</p></td>
<td><p>Cart detect. Z: No cart, NZ: Cart inserted (Test Register 0x53 Bit 1 and invert Zero flag)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$3E</p></td>
<td><p>007C:0B2E</p></td>
<td><p>Read structure, write 0xFF, compare values and optionally jump to subroutine<br />
X point to a structure in memory:</p>
<p><code>structure {</code><br />
<code> byte   type            ; 0x01 = Call subroutine, 0x00 = Don't call subroutine</code><br />
<code> triple write_0xFF_addr ; Address that 0xFF will be written</code><br />
<code> triple compare_addr    ; Address to read for compare</code><br />
<code> byte   compare_value   ; Value that must match the compare</code><br />
<code> triple subroutine      ; Use byte POP to receive flag of the compare</code><br />
<code>}</code><br />
<code>if type is 0x00, register A return 0x01 if compare is equal</code></p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$3F</p></td>
<td><p>007E:0B8F</p></td>
<td><p>Set PRC Rate (A = 0 to 7)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$40</p></td>
<td><p>0080:0BA3</p></td>
<td><p>Get PRC Rate (return A)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$41</p></td>
<td><p>0082:0BB1</p></td>
<td><p>Test cart type. Returns Z: non multi cart, NZ: multi cart (Register 0x01 Bit 3)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$42</p></td>
<td><p>0084:047A</p></td>
<td><p>Nintendo Dev Card (Read IDs)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$43</p></td>
<td><p>0086:0493</p></td>
<td><p>Nintendo Dev Card (Reset)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$44</p></td>
<td><p>0088:04A4</p></td>
<td><p>Nintendo Dev Card (Program Byte)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$45</p></td>
<td><p>008A:04C8</p></td>
<td><p>Nintendo Dev Card (Erase Sector)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$46</p></td>
<td><p>008C:04F5</p></td>
<td><p>Nintendo Dev Card (Unlock flash page register. Command 0xD0)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$47</p></td>
<td><p>008E:0506</p></td>
<td><p>Nintendo Dev Card (Select flash bank. A=bank Nr, X last address of flash page)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$48</p></td>
<td><p>0090:0517</p></td>
<td><p>Nintendo Dev Card (Command 0xC9)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$49</p></td>
<td><p>0092:0529</p></td>
<td><p>Nintendo Dev Card (Prepare Manufacturer and device ID readout. Command 0xC0)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$4A</p></td>
<td><p>0094:053A</p></td>
<td><p>Nintendo Dev Card (Select flash game. A = game Nr. ([0x041048 + 96 * A] if 0x08 -&gt; Command 0xC9)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>$4B</p></td>
<td><p>0096:0000</p></td>
<td><p>Nintendo SDK</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>$4C</p></td>
<td><p>0098:0BBD</p></td>
<td><p>IR pulse MOV [Y], $02 ; wait B*16 Cycles ; MOV [Y], $00</p></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>