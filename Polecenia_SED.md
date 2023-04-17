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
		<td align="left">[^aeiou]</td>
		<td align="left">any except vovels</td>
	</tr>
	<tr>
		<td align="left">*</td>
		<td align="left">Zero or more copies</td>
	</tr>
	<tr>
		<td align="left">[a-z]\{4,8\}</td>
		<td align="left">a-z from 4 to 8</td>
	</tr>
</tbody>
</table>
<table border="">
	<tbody><tr>
		<td align="center">Regular Expression</td>
		<td>Class</td>
		<td>Type</td>
		<td>Meaning</td>
	</tr>
	<tr>
		<td align="left">_</td>
	</tr>
	<tr>
		<td align="left">.</td>
		<td align="left">all</td>
		<td align="left">Character Set</td>
		<td align="left">A single character (except newline)</td>
	</tr>
	<tr>
		<td align="left">^</td>
		<td align="left">all</td>
		<td align="left">Anchor</td>
		<td align="left">Beginning of line</td>
	</tr>
	<tr>
		<td align="left">$</td>
		<td align="left">all</td>
		<td align="left">Anchor</td>
		<td align="left">End of line</td>
	</tr>
	<tr>
		<td align="left">[...]</td>
		<td align="left">all</td>
		<td align="left">Character Set</td>
		<td align="left">Range of characters</td>
	</tr>
	<tr>
		<td align="left">*</td>
		<td align="left">all</td>
		<td align="left">Modifier</td>
		<td align="left">zero or more duplicates</td>
	</tr>
	<tr>
		<td align="left">\&lt;</td>
		<td align="left">Basic</td>
		<td align="left">Anchor</td>
		<td align="left">Beginning of word</td>
	</tr>
	<tr>
		<td align="left">\&gt;</td>
		<td align="left">Basic</td>
		<td align="left">Anchor</td>
		<td align="left">End of word</td>
	</tr>
	<tr>
		<td align="left">\(..\)</td>
		<td align="left">Basic</td>
		<td align="left">Backreference</td>
		<td align="left">Remembers pattern</td>
	</tr>
	<tr>
		<td align="left">\1..\9</td>
		<td align="left">Basic</td>
		<td align="left">Reference</td>
		<td align="left">Recalls pattern</td>
	</tr>
	<tr>
		<td align="left">_+</td>
		<td align="left">Extended</td>
		<td align="left">Modifier</td>
		<td align="left">One or more duplicates</td>
	</tr>
	<tr>
		<td align="left">?</td>
		<td align="left">Extended</td>
		<td align="left">Modifier</td>
		<td align="left">Zero or one duplicate</td>
	</tr>
	<tr>
		<td align="left">\{M,N\}</td>
		<td align="left">Extended</td>
		<td align="left">Modifier</td>
		<td align="left">M to N Duplicates</td>
	</tr>
	<tr>
		<td align="left">(...|...)</td>
		<td align="left">Extended</td>
		<td align="left">Anchor</td>
		<td align="left">Shows alteration</td>
	</tr>
	<tr>
		<td align="left">_</td>
	</tr>
	<tr>
		<td align="left">\(...\|...\)</td>
		<td align="left">EMACS</td>
		<td align="left">Anchor</td>
		<td align="left">Shows alteration</td>
	</tr>
	<tr>
		<td align="left">\w</td>
		<td align="left">EMACS</td>
		<td align="left">Character set</td>
		<td align="left">Matches a letter in a word</td>
	</tr>
	<tr>
		<td align="left">\W</td>
		<td align="left">EMACS</td>
		<td align="left">Character set</td>
		<td align="left">Opposite of \w</td>
	</tr>
</tbody></table>
