---
id: gme8nq5edv12pfupo16brtb
title: Datatypes
desc: ''
updated: 1647154736945
created: 1647131823857
---
## Data Types

### Integral Numeric Types

<table aria-label="Characteristics of the integral types" class="table table-sm">
<thead>
<tr>
<th>C# type/keyword</th>
<th>Range</th>
<th>Size</th>
<th>.NET type</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>sbyte</code></td>
<td>-128 to 127</td>
<td>Signed 8-bit integer</td>
<td><a href="/en-us/dotnet/api/system.sbyte" class="no-loc" data-linktype="absolute-path">System.SByte</a></td>
</tr>
<tr>
<td><code>byte</code></td>
<td>0 to 255</td>
<td>Unsigned 8-bit integer</td>
<td><a href="/en-us/dotnet/api/system.byte" class="no-loc" data-linktype="absolute-path">System.Byte</a></td>
</tr>
<tr>
<td><code>short</code></td>
<td>-32,768 to 32,767</td>
<td>Signed 16-bit integer</td>
<td><a href="/en-us/dotnet/api/system.int16" class="no-loc" data-linktype="absolute-path">System.Int16</a></td>
</tr>
<tr>
<td><code>ushort</code></td>
<td>0 to 65,535</td>
<td>Unsigned 16-bit integer</td>
<td><a href="/en-us/dotnet/api/system.uint16" class="no-loc" data-linktype="absolute-path">System.UInt16</a></td>
</tr>
<tr>
<td><code>int</code></td>
<td>-2,147,483,648 to 2,147,483,647</td>
<td>Signed 32-bit integer</td>
<td><a href="/en-us/dotnet/api/system.int32" class="no-loc" data-linktype="absolute-path">System.Int32</a></td>
</tr>
<tr>
<td><code>uint</code></td>
<td>0 to 4,294,967,295</td>
<td>Unsigned 32-bit integer</td>
<td><a href="/en-us/dotnet/api/system.uint32" class="no-loc" data-linktype="absolute-path">System.UInt32</a></td>
</tr>
<tr>
<td><code>long</code></td>
<td>-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807</td>
<td>Signed 64-bit integer</td>
<td><a href="/en-us/dotnet/api/system.int64" class="no-loc" data-linktype="absolute-path">System.Int64</a></td>
</tr>
<tr>
<td><code>ulong</code></td>
<td>0 to 18,446,744,073,709,551,615</td>
<td>Unsigned 64-bit integer</td>
<td><a href="/en-us/dotnet/api/system.uint64" class="no-loc" data-linktype="absolute-path">System.UInt64</a></td>
</tr>
<tr>
<td><code>nint</code></td>
<td>Depends on platform</td>
<td>Signed 32-bit or 64-bit integer</td>
<td><a href="/en-us/dotnet/api/system.intptr" class="no-loc" data-linktype="absolute-path">System.IntPtr</a></td>
</tr>
<tr>
<td><code>nuint</code></td>
<td>Depends on platform</td>
<td>Unsigned 32-bit or 64-bit integer</td>
<td><a href="/en-us/dotnet/api/system.uintptr" class="no-loc" data-linktype="absolute-path">System.UIntPtr</a></td>
</tr>
</tbody>
</table>

### Floating Point Numeric Types

<table aria-label="Characteristics of the floating-point types" class="table table-sm">
<thead>
<tr>
<th>C# type/keyword</th>
<th>Approximate range</th>
<th>Precision</th>
<th>Size</th>
<th>.NET type</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>float</code></td>
<td>±1.5 x 10<sup>−45</sup> to ±3.4 x 10<sup>38</sup></td>
<td>~6-9 digits</td>
<td>4 bytes</td>
<td><a href="/en-us/dotnet/api/system.single" class="no-loc" data-linktype="absolute-path">System.Single</a></td>
</tr>
<tr>
<td><code>double</code></td>
<td>±5.0 × 10<sup>−324</sup> to ±1.7 × 10<sup>308</sup></td>
<td>~15-17 digits</td>
<td>8 bytes</td>
<td><a href="/en-us/dotnet/api/system.double" class="no-loc" data-linktype="absolute-path">System.Double</a></td>
</tr>
<tr>
<td><code>decimal</code></td>
<td>±1.0 x 10<sup>-28</sup> to ±7.9228 x 10<sup>28</sup></td>
<td>28-29 digits</td>
<td>16 bytes</td>
<td><a href="/en-us/dotnet/api/system.decimal" class="no-loc" data-linktype="absolute-path">System.Decimal</a></td>
</tr>
</tbody>
</table>

### Boolean

`bool`

### Char

`char`

### Strings

`string`
