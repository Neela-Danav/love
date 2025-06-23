.. _sast_scans:

======================
Performing a SAST Scan
======================

The ``pysast`` module can also be used as a command line utility. It provides a convenient
way to perform Static Application Security Testing (SAST) scans on one or more files or
directories. This comprehensive guide will walk you through the various options and
functionalities of ``pysast``, enabling you to leverage its power for effective code
analysis and vulnerability detection.

Command syntax
--------------

The general syntax for using pysast is as follows:

.. code:: shell

    pysast [-h] [-r] [-j] [-v] [-s SAST_RULES] [-S SAST_DIRS] [-rS] \
        [--disable-prefilter] [--enable-postfilter] [-M MAX_BYTES] [PATHS ...]

Let's explore the available options and their functionalities:

Positional Arguments
~~~~~~~~~~~~~~~~~~~~

- ``PATHS``:
    One or more files or directories to scan. Specify the path(s) to the file(s) or
    directory(ies) you want ``pysast`` to analyze.

Options
~~~~~~~

-h, --help
 Displays the help message and exits.

-r, --recursive
 Scan target directories recursively. This option enables pysast to scan
 files within the specified directories and their subdirectories.

-j, --json
 Dump JSON output instead of using pprint. Use this option if you prefer
 the scan results in JSON format.

-v, --verbose
 Specifies the verbosity for the next scan. You can use -v for verbose
 output and -vvv for more detailed and verbose output.

-s SAST_RULES, --sast-rule SAST_RULES
 Specifies the file path(s) to the SAST rules you want to import. You can
 provide one or more file paths separated by spaces. This option allows you
 to use custom SAST rules for the scan.

-S SAST_DIRS, --sast-dir SAST_DIRS
 Specifies one or more directories that store SAST rules. You can provide
 one or more directory paths separated by spaces. Use this option when your
 SAST rules are stored in directories instead of individual files. The
 current directory is used if no rules are specified.

-rS, --recursive-sast-dir
 Load rules from target directories recursively. When using this option,
 ``pysast`` will search for SAST rules in the specified directories and
 their subdirectories.

--disable-prefilter
 Disable prefiltering rules. By default, pysast applies a prefiltering
 step to improve the performance of the scan. Use this option if you want
 to disable the prefiltering step.

--enable-postfilter
 Enable postfiltering. This option allows pysast to apply additional filtering
 on the scan results, further refining the output.

-M MAX_BYTES, --max-bytes MAX_BYTES
 Skip files exceeding the specified maximum bytes. Use this option to set a
 threshold for the file size. Files larger than the specified maximum bytes
 will be skipped during the scan.
-T, --disable-mime
Specifies whether the scanner should use the 'file' utility to retrieve the
MIME-type of a file. (enabled as per default)
-e EXCLUDE_FILES, --exclude-file EXCLUDE_FILES
Specifies exclusion files (use re: for regular expressions)
--threading
Activates threading for file processing. (Can't be used on daemon processes)


Usage Examples
--------------

Let's look at some examples of using pysast with different options:

.. note::
    If no path or directory to rules is given, the current directory will be
    scanned for rule definitions.

- Scan a single file:

    .. code:: bash

        pysast path/to/file.py

- Scan multiple files:

    .. code:: bash

        pysast path/to/file1.py path/to/file2.py path/to/file3.py

- Scan a directory recursively:

    .. code:: bash

        pysast -r path/to/directory

- Scan a directory with custom SAST rules:

    .. code:: bash

        pysast -s path/to/rules.json path/to/directory

- Scan a directory with SAST rules stored in a directory:

    .. code:: bash

        pysast -S path/to/rules_directory path/to/directory

- Scan a directory with recursively loaded SAST rules:

    .. code:: bash

        pysast -rS path/to/rules_directory path/to/directory

- Scan with verbose output:

    .. code:: bash

        pysast -v path/to/file.py

- Scan with JSON output:

    .. code:: bash

        pysast -j path/to/file.py

- Scan with maximum file size limit:

    .. code:: bash

        pysast -M 10000 path/to/file.py

These examples demonstrate some common usage scenarios of pysast. You can
combine multiple options to tailor the scan according to your specific needs.

Program Optimization with Threading
-----------------------------------

Since version ``1.1.0`` this program introduces an optimization feature that significantly
improves its performance by leveraging threading. By utilizing the ``--threading`` option
on the command line, you can enable this optimization to take full advantage of your
system's resources.

How It Works
~~~~~~~~~~~~

The optimization primarily targets the ``scan_dir()`` function, which scans a directory and
its subdirectories for files. The original implementation sequentially scans each file,
resulting in potential performance bottlenecks, especially for larger directories.

With the optimization enabled, the program utilizes threading to parallelize the scanning
process. By utilizing concurrent execution, multiple files can be scanned simultaneously,
making efficient use of available CPU cores and drastically reducing the overall execution
time.

Usage
~~~~~

To enable the optimization, simply append the ``--threading`` option when executing the program
from the command line. For example:

- Scan a directory recursively with threading enabled:

    .. code:: bash

        pysast --threading -r path/to/directory


.. note::
    It's important to measure the impact of the optimization in your specific use case. While
    threading can significantly enhance performance for CPU-bound tasks, it may not always provide
    improvements in scenarios where the program is I/O-bound or subject to certain limitations.
    Therefore, we recommend benchmarking and profiling your program to evaluate the effectiveness
    of the optimization in your particular environment.