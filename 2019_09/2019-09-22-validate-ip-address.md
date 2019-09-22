#### 题目：判断ip地址是否合法
IPv4地址以点十进制表示法规范表示，点十进制表示法由四个十进制数字组成，每个数字的范围为0至255，并用点（“.”）分隔，例如172.16.254.1；

此外，IPv4中的前导零是无效的。例如，地址172.16.254.01无效。

IPv6地址表示为八组的四个十六进制数字，每组代表16位。这些组用冒号（“:”）分隔。例如，该地址2001:0db8:85a3:0000:0000:8a2e:0370:7334是有效地址。同样，我们可以忽略四个十六进制数字中的一些前导零，并将地址中的一些小写字符改为大写，因此2001:db8:85a3:0:0:8A2E:0370:7334也是有效的IPv6地址（忽略前导零并使用大写）。

但是，我们不使用两个连续的冒号（：:)来将单个零值的连续组替换为一个空组，以追求简单性。例如，2001:0db8:85a3::8A2E:0370:7334是无效的IPv6地址。

此外，IPv6中多余的前导零也是无效的。例如，地址02001:0db8:85a3:0000:0000:8a2e:0370:7334无效。

注意： 您可以假定输入字符串中没有多余的空格或特殊字符。？

#### 思路：先判断是否为IPv4地址，再判断是否为IPv6地址，如果都不是返回“Neither”。
代码：
```
class Solution {
    public String validIPAddress(String IP) {
        if (isIPv4(IP)) {
            return "IPv4";
        } else if (isIPv6(IP)) {
            return "IPv6";
        }
        return "Neither";
    }
    public Boolean isIPv4(String IP) {
        if (IP == null || IP.length() < 7 || IP.endsWith(".")) {
            return false;
        }
        String[] arr = IP.split("\\.");
        if (arr.length == 4) {
            for (String item : arr) {
                if (item.startsWith("-") || item.length() > 1 && item.startsWith("0")) {
                    return false;
                }
                try {
                    int n = Integer.parseInt(item);
                    if (n < 0 || n > 255) {
                        return false;
                    }
                } catch (Exception e) {
                    return false;
                }
            }
            return true;
        }
        return false;
    }
    public Boolean isIPv6(String IP) {
        if (IP == null || IP.length() < 15 || IP.endsWith(":")) {
            return false;
        }
        String[] arr = IP.split(":");
        if (arr.length == 8) {
            for (String item : arr) {
                if (item.length() <= 0 || item.length() > 4) {
                    return false;
                }
                for (int i = 0; i < item.length(); i++) {
                    char c = item.charAt(i);
                    if (!(c >= '0' && c <= '9' || c >= 'a' && c <= 'f' || c >= 'A' && c <= 'F')) {
                        return false;
                    }
                }
            }
            return true;
        }
        return false;
    }
}
```
