---
title: Functions Defined by Printer Graphics DLLs
author: windows-driver-content
description: Functions Defined by Printer Graphics DLLs
ms.assetid: b0c9ce45-76c4-4058-af3f-7b9d230bcf94
keywords:
- printer graphics DLL WDK , functions
- functions WDK printer graphics DLL
- graphics DLL WDK printer , functions
ms.date: 04/20/2017
ms.localizationpriority: medium
---

# Functions Defined by Printer Graphics DLLs





Like all graphics drivers, printer graphics DLLs are responsible for defining the following graphics DDI functions. Following [**DrvEnableDriver**](https://msdn.microsoft.com/library/windows/hardware/ff556210), the initial driver entry point, the remaining functions are listed in alphabetical order. Note that because GDI calls **DrvEnableDriver** by name, its name appears in bold. GDI calls all other display driver functions by way of an array of function pointers that **DrvEnableDriver** returns.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Function Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[<strong>DrvEnableDriver</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556210)</p></td>
<td><p>Allows the driver to initialize itself and return pointers to supported graphics DDI functions.</p></td>
</tr>
<tr class="even">
<td><p>[<strong>DrvCompletePDEV</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556181)</p></td>
<td><p>Provides the driver with a GDI handle to a device instance.</p></td>
</tr>
<tr class="odd">
<td><p>[<strong>DrvDisableDriver</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556196)</p></td>
<td><p>(Optional) Allows the driver to perform cleanup operations before being unloaded.</p></td>
</tr>
<tr class="even">
<td><p>[<strong>DrvDisablePDEV</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556198)</p></td>
<td><p>Allows the driver to remove device instance-specific information.</p></td>
</tr>
<tr class="odd">
<td><p>[<strong>DrvDisableSurface</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556200)</p></td>
<td><p>Allows the driver to remove a drawing surface.</p></td>
</tr>
<tr class="even">
<td><p>[<strong>DrvEnablePDEV</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556211)</p></td>
<td><p>Allows the driver to provide GDI with physical device characteristics and to initialize device instance-specific information.</p></td>
</tr>
<tr class="odd">
<td><p>[<strong>DrvEnableSurface</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556214)</p></td>
<td><p>Allows the driver to create a drawing surface.</p></td>
</tr>
<tr class="even">
<td><p>[<strong>DrvQueryDeviceSupport</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556260)</p></td>
<td><p>(Optional) Returns requested device-specific information.</p></td>
</tr>
<tr class="odd">
<td><p>[<strong>DrvQueryDriverInfo</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556261)</p></td>
<td><p>(Optional) Returns requested driver-specific information.</p></td>
</tr>
</tbody>
</table>

 

Printer graphics DLLs are also responsible for defining the following print-specific graphics DDI functions, which are called at certain points during the rendering of a print job.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Function</th>
<th>When Called</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[<strong>DrvEndDoc</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556215)</p></td>
<td><p>When GDI has finished sending a document to the driver for rendering.</p></td>
</tr>
<tr class="even">
<td><p>[<strong>DrvNextBand</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556250)</p></td>
<td><p>(Optional) When GDI has finished drawing a band for a physical page, so the driver can send the band to the printer.</p></td>
</tr>
<tr class="odd">
<td><p>[<em>DrvQueryPerBandInfo</em>](https://msdn.microsoft.com/library/windows/hardware/ff556268)</p></td>
<td><p>(Optional) Before GDI begins drawing a band for a physical page, so the driver can supply GDI with band-specific information.</p></td>
</tr>
<tr class="even">
<td><p>[<em>DrvSendPage</em>](https://msdn.microsoft.com/library/windows/hardware/ff556281)</p></td>
<td><p>When GDI has finished drawing a physical page, so the driver can send the page to the printer.</p></td>
</tr>
<tr class="odd">
<td><p>[<strong>DrvStartBanding</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556292)</p></td>
<td><p>(Optional) When GDI is ready to start sending bands of a physical page to the driver for rendering.</p></td>
</tr>
<tr class="even">
<td><p>[<strong>DrvStartDoc</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556296)</p></td>
<td><p>When GDI is ready to start sending a document to the driver for rendering.</p></td>
</tr>
<tr class="odd">
<td><p>[<strong>DrvStartPage</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556298)</p></td>
<td><p>When GDI is ready to start sending a document page to the driver for rendering.</p></td>
</tr>
</tbody>
</table>

 

Typically, a printer graphics DLL also defines whatever additional graphics DDI functions are necessary to accomplish print job rendering. The number and type of functions defined depends on:

-   Whether the driver supports use of GDI-managed or device-managed drawing surfaces (or both). For more information, see [Surface Types](https://msdn.microsoft.com/library/windows/hardware/ff569900).

-   The extent to which drawing operations can be handled by GDI instead of being performed by the driver itself. For more information, see [Using the Graphics DDI](https://msdn.microsoft.com/library/windows/hardware/ff570139).

All functions defined by printer graphics DLLs are called by GDI's kernel-mode graphics rendering engine (GRE).

The [**DrvEnableDriver**](https://msdn.microsoft.com/library/windows/hardware/ff556210) and [**DrvQueryDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff556261) functions are exported by the graphics DLL. The addresses of all other supported graphics DDI functions are placed in a table that is returned by the **DrvEnableDriver** function.

 

 




