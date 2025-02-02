---
title: Plugin - I/O Parser
permalink: /docs/io_parser/
---

The integrated parser API for plugins provides a way to build __expression chains__ in order to extract some interest value of output files in a directory. An expresison chain is a sequence of function calls `f(...)  >> g(...) >> h(...)`, where the first argument of each secondary function (`g` and `h`) is the result of the previous one.


For instance `grep("(.*)out"," z=") >> get(0) >> between("z=","|") >> asNumeric()` will process as follows:

* `grep("(.*)out"," z=")`: find __all__ lines containing ' z=' in __all__ files which name ends with "out" (in the current working directory, usually 'output/'),
* `>> get(0)`: from this list of lines, get the the __last__ one,
* `>> between("z=","|")`: from this line, get the substring between `z=` and `|`,
* `>> asNumeric()`: parse this string and cast as a numeric value.

The built-in functions available in the parser are the following (`grep "public static" ../funz-core/src/main/java/org/funz/util/Parser.java`):

* _note that first argument is in fact the result of previous function (if it exists)_
* _`List<...>` are processed by later function iteratively_

* `List<File> unzip(File z)`
* `List<String> CSV(List<String> lines, String delim, String title)`
* `String JSONPath(File file, String path)`
* `String XPath(File file, String path)`
* `String toString(Document xml)`
* `List<String> toStrings(List<Document> xml)`
* `String filecat(File f)`
* `String property(File f, String key)`
* `List<String> grep(File file, String keyfilter)`
* `List<String> grepIn(String input, String keyfilter)`
* `List<String> grep(BufferedReader inn, String keyfilter)`
* `List<String> grep_basic(BufferedReader inn, String keyfilter)`
* `List<String> gnotrep(BufferedReader inn, String keyfilter)`
* `Boolean contains(File file, String keyfilter)`
* `Boolean containsIn(String input, String keyfilter)`
* `Boolean contains(BufferedReader inn, String keyfilter)`
* `List<String> filter(List<String> lines, String regexp)`
* `int[] filterIndexes(List<String> lines, String regexp)`
* `String strcat(String... lines)`
* `String strcat(LinkedList lines)`
* `String cat(List lines, String separator)`
* `List<String> merge(List lines)`
* `int length(String line)`
* `List<Integer> length(List<String> lines)`
* `String trim(String line)`
* `List<String> trim(List<String> lines)`
* `List<String> split(String line, String separator)`
* `String cut(String line, String separator, int index)`
* `List<String> cut(List<String> lines, String separator, int index)`
* `String substring(String line, int begin, int end)`
* `String substring(String line, String beginstr, String endstr)`
* `List<String> substring(List<String> lines, int begin, int end)`
* `List<String> substring(List<String> lines, String beginstr, String endstr)`
* `String substring(String line, int begin)`
* `String substring(String line, String beginstr)`
* `List<String> substring(List<String> lines, int begin)`
* `List<String> substring(List<String> lines, String beginstr)`
* `String replace(String line, String toreplace, String replacer)`
* `List<String> replace(List<String> lines, String toreplace, String replacer)`
* `String replace_regexp(String line, String toreplace, String replacer)`
* `List<String> replace_regexp(List<String> lines, String toreplace, String replacer)`
* `String after(String line, String beginstr)`
* `List<String> after(List<String> lines, String beginstr)`
* `String afterLast(String line, String beginstr)`
* `List<String> afterLast(List<String> lines, String beginstr)`
* `String before(String line, String endstr)`
* `List<String> before(List<String> lines, String beginstr)`
* `String between(String line, String beginstr, String endstr)`
* `List<String> between(List<String> lines, String beginstr, String endstr)`
* `List<String> get(List<String> lines, int... numbers)`
* `List<String> getAfter(List<String> lines, int after, int... numbers)`
* `List<String> getBefore(List<String> lines, int before, int... numbers)`
* `String get(List<String> lines, int i)`
* `List<String> getBy(List<String> lines, int start, int step)`
* `List<String> getBy(List<String> lines, int start, int step, int end)`
* `List<String> getAll(List<List<String>> lines, int i)`
* `double times(double d, double t)`
* `double[] times(double[] d, double t)`
* `double[][] times(double[][] d, double t)`
* `double asNumeric(String line)`
* `double asNumeric(List line)`
* `double[] asNumeric1DArray(String line, String delim)`
* `double[] asNumeric1DArray(String line)`
* `double[] asNumeric1DArray(List<String> lines)`
* `double[][] asNumeric2DArray(String line, String coldelim, String rowdelim)`
* `double[][] asNumeric2DArray(String line)`
* `double[][] asNumeric2DArray(List<String> lines, String coldelim)`
* `double[][] asNumeric2DArray(List<String> lines)`