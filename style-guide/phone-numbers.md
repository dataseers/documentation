# Phone numbers

Phone numbers around the world can range from only four digits all the way up to seventeen. However, must phone numbers will be in the 7-10 digit range. A phone number consists of the following parts:

<dl>
  <dt><b>Exit Code</b></dt>
  <dd>
    An exit code is placed at the beginning of a phone number. It notifies your telecom carrier that you're about to place a call outside of your home country. For example, the exit code in the United States and Canada is 011. However, you can bypass this altogether by using a plus "+" in place of the exit code. If we did +91, then that gets converted to 011 39 when calling from within the United States.
  </dd>
  <dt><b>Country Code</b></dt>
  <dd>
    A country code identifies the country that a phone number belongs to. This code allows your telecom carrier to connect to a carrier in the country you're trying to reach. In the last example, we used +91. 91 would be the country code for India.
  </dd>
  <dt><b>Area code</b></dt>
  <dd>
    An area code identifies which specific geographic area a phone number belongs to. Some area codes cover multiple towns in the same region while others are just one of many area codes used by a single large city.
  </dd>
  <dt><b>Local number</b></dt>
  <dd>
    A local number in a North American Numbering Plan consists of an <b>exchange code</b> and a <b>line number</b>. However, with the inclusion of international numbers, the local number refers to all the remaining digits of a phone number.
  </dd>
  <dt><b>Extension</b></dt>
  <dd>
    An extension is a short numeric code added to a main phone number to direct calls to a specific person or department within an organization.
  </dd>
</dl>

## Formatting phone numbers

### NANP numbers

The North American Numbering Plan or NANP is a numbering plan used primarily in North America and the Caribbean. However, Mexico does not participate in NANP. Phone numbers from this region will have the following formatting rules:

- Area code enclosed with parentheses
- Hyphenate the three-digit exchange code with the four-digit line number

```
# Syntax
(<AREA_CODE>) <EXCHANGE_CODE>-<LINE_NUMBER>

# Example
(678) 421-4217
```

### International numbers

International numbers will start with the exit and country codes. The area code will still be enclosed with parentheses

- Exit code followed by the country code with no space between
- Area code enclosed with parentheses
- Local number without any additional formatting

```
# Syntax
+<COUNTRY_CODE> (<AREA_CODE>) <LOCAL_NUMBER>

# Example
+91 (22) 12345678
+52 (555) 12345678
```

### Alternate formats

If the above formats prove too difficult to implement, then we could use the E.164 format which is a global standard. The formatting rules are:

- Exit code followed by the country code with no space between
- Area code and local number combined with no spaces

The simplicity of the layout also has the drawback of making phone numbers more difficult to read.

```
# Syntac
+<COUNTRY_CODE> <AREA_CODE><LOCAL_NUMBER>

# Example
+91 2212345678
+52 55512345678
```
