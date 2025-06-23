.. _sast_rules:

==================
Writing SAST Rules
==================

This guide aims to provide you with a comprehensive understanding of Static Application
Security Testing (SAST) rules and how to effectively write them. SAST rules play a crucial
role in identifying potential security vulnerabilities, coding flaws, and adherence to
coding standards within your software applications.

.. note::
    It's important to note that SAST rules alone cannot guarantee the absence of vulnerabilities
    in your code. They are an important part of a comprehensive security strategy, which should
    also include other testing methodologies, secure coding practices, and ongoing security
    assessments.

Benefits of Writing SAST Rules
------------------------------

Creating effective SAST rules offers several benefits throughout the software development
lifecycle:

1. Early Detection of Vulnerabilities:
    By implementing SAST rules, you can identify security vulnerabilities at an early stage,
    allowing developers to address them before deployment. This saves time, effort, and
    potential reputational damage.

2. Improved Code Quality:
    SAST rules not only focus on security but also enforce coding best practices. Following
    these practices enhances code quality, maintainability, and reduces the likelihood of
    introducing new vulnerabilities.

3. Consistent Security Standards:
    SAST rules enable you to enforce consistent security standards across your development
    team and projects. This ensures that all code undergoes a standardized security review
    process.


Rule Format
-----------

Let's take a quick look at the overall structure of a SAST rule:

.. code-block:: json

    "<rule-id>": {
        "input": "default|lower|upper",
        "pattern": {
            "engine": "re",
            "text": "<pattern_text>",
            "mode": "and|or|not"
        },
        "meta": {
            "description": "<rule_description>",
            "severity": "<rule_severity>",
            "title": "<rule_title>",
            "filter": {
                "file_ext": "<file_extension>",
                "mime_type": "<mime_type>",
                "file_path": "<file_path>",
                "file_name": "<file_name>"
            }
        }
    }

This is the format for defining a rule in the rule set. Rules are used for static
application security testing (SAST) to detect specific patterns in code or files.
Each rule is identified by a unique "rule-id" string.

.. important::
    In addition to JSON, a rule can also be defined using YAML format.

Rule Properties
~~~~~~~~~~~~~~~

- ``input``:
    Specifies the transformation to be applied to the input before matching the
    pattern. Valid values are ``default``, ``lower``, or ``upper``.

- ``pattern``:
    Contains information about the pattern to be matched. Definition can be either
    a single string or an object storing the pattern string with extra options.

- ``patterns``:
    A list of pattern definitions.

- ``engine``:
    Specifies the pattern matching engine to be used. Currently, only regular
    expression (``re``) engine is supported.

- ``text``:
    The actual pattern text to be matched using the specified engine.

- ``mode``:
    Specifies the matching mode for the pattern. Valid values are ``and``, ``or``,
    or ``not``. Multiple patterns within a rule can be combined using these modes
    using a ``+``.

- ``meta``:
    Contains metadata information for the rule.

    - ``description``:
        A description of the rule, providing details about its purpose or behavior.

    - ``severity``:
        Specifies the severity level of the rule, indicating the importance or impact
        of violations detected by the rule.

    - ``title``:
        The title or name of the rule.

    - ``filter``:
        Contains filter criteria to further narrow down the files or code elements to
        be analyzed by the rule.

        - ``file_ext``:
            Specifies the file extension filter. Only files with the specified extension
            will be considered for analysis.
        - ``mime_type``:
            Specifies the MIME type filter. Only files with the specified MIME type will
            be considered for analysis.
        - ``file_path``:
            Specifies the file path filter. Only files matching the specified path pattern
            will be considered for analysis.
        - ``file_name``:
            Specifies the file name filter. Only files with the specified name pattern
            will be considered for analysis.

Usage
-----

To define a rule, just replace the placeholders in the rule format with actual values.
The ``rule-id`` should be unique within the rule set. The "input" property is set
to "default" if no transformation is required on the input and can be left out.

Specify the desired pattern, pattern engine, and matching mode in the "pattern" section,
where the pattern engine and matching mode are optional. For instance, the next three code
examples will return the same result:

.. code-block:: json
    :caption: String definition (``re``-Engine used)

    "rule-id": {
        "pattern": "ISSUE_[A_Z]+"
    }

.. code-block:: yaml
    :caption: Full definition

    - rule-id: <id> # advanced
        pattern:
          text: ISSUE_[A-Z]+
          engine: my_custom_module
          mode: not # this pattern must NOT occur in a scanned file

    - rule-id: <id> # simple
        pattern:
          # "and" will be set as default mode and "re" as engine
          text: ISSUE_[A-Z]+


.. code-block:: json
    :caption: or definition within a list (use string or full definition)

    "<rule-id>": {
        "patterns": [
            "ISSUE_[A-Z]+"
        ]
    }


Provide a meaningful description, severity, and title in the ``meta`` section.
Optionally, add filter criteria in the ``filter`` section to narrow down the
analysis scope of the rule. The filter can be applied as follows:

.. code-block:: yaml

    - rule-id: example-rule
      meta:
        filters:
          # mime-type != text/html or mime-type != text/json
          mime_type: "!text/html,text/json"
          # re.match(r"xml.*", extension)
          file_ext: re:xml.*
          # file_name == "README"
          file_name: README
          # not re.match(r".*/src.*", file_path)
          file_path: "!re:.*/src.*"


Example
-------

.. code-block:: json

    {
        "example-rule": {
            "input": "lower",
            "pattern": {
                "engine": "re",
                "text": "security_[A-Z]+_issue",
                "mode": "and"
            },
            "meta": {
                "description": "Detects security-related issues with a specific naming convention.",
                "severity": "high",
                "title": "Security Naming Convention"
            }
        }
    }

Or the same rule in YAML format (note that optional settings are left out):

.. code-block:: yaml

    - rule-id: example-rule
      input: lower
      pattern: security_[A-Z]+_issue
      meta:
        description: Detects security-related issues with a specific naming convention.
        severity: high
        title: Security Naming Convention
