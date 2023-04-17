# `SED`
is the ultimate `S`tream `ED`itor and is line oriented (only first occurrence is changed)

## S for Substitution
sed 's/day/night/' old >new

Zamienia słowa `day` na `night` w pliku `old` i nadpisuje je (>) w pliku `new`.

## Delimeter - ogranicznik
's/\/usr\/local\/bin/\/common\/bin/'

's_/usr/local/bin_/common/bin_'

's:/usr/local/bin:/common/bin:'

's|/usr/local/bin|/common/bin|'

## Unix RegExp - Basic Type

<table border="">
	<tbody><tr>
		<td align="center">Pattern</td>
		<td>Matches</td>
	</tr>
	<tr>
		<td align="left">^A</td>
		<td align="left">"A" at the beginning of a line</td>
	</tr>
	<tr>
		<td align="left">A$</td>
		<td align="left">"A" at the end of a line</td>
	</tr>
	<tr>
		<td align="left">A^</td>
		<td align="left">"A^" anywhere on a line</td>
	</tr>
	<tr>
		<td align="left">$A</td>
		<td align="left">"$A" anywhere on a line</td>
	</tr>
	<tr>
		<td align="left">^^</td>
		<td align="left">"^" at the beginning of a line</td>
	</tr>
	<tr>
		<td align="left">$$</td>
		<td align="left">"$" at the end of a line</td>
	</tr>
    <tr>
		<td align="left">.</td>
		<td align="left">"." any single character</td>
	</tr>
    <tr>
		<td align="left">^[0-9]$</td>
		<td align="left">Range of numbers</td>
	</tr>
    </tr>
    <tr>
		<td align="left">[A-Za-z0-9_]</td>
		<td align="left">names</td>
	</tr>
</tbody>
</table>
