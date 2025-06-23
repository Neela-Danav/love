.. pysast documentation master file, created by
   sphinx-quickstart on Fri May 19 15:37:51 2023.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to pysast's documentation!
==================================

.. contents::

Welcome to the documentation for ``pysast`` - a powerful Python package designed for
scanning one or multiple files using customizable rules written in JSON or YAML. With
``pysast``, you can easily automate the process of code analysis and identify potential
issues or violations based on your specified criteria.

``pysast`` provides a user-friendly and intuitive interface for integrating static
analysis into your projects. By utilizing the rule-based system, you can define a set of
rules that reflect your desired coding standards, best practices, or specific requirements.
The package can scans your files, identifies instances that violate the defined rules, and
reports them to help you maintain a high code quality.

Key Features
------------

- Flexible Rule Definition:
   ``pysast`` allows you to define rules in either JSON or YAML format, providing flexibility
   and ease of use for expressing your desired code analysis criteria. You can find more
   information on how to write rules in the :doc:`Writing SAST Rules <intro/sast_rules>` document.

- File Scanning:
   With ``pysast``, you can scan one or multiple files with a single command, saving you time
   and effort in manually checking each file for adherence to your coding standards.

- Customizable Rules:
   Tailor the analysis to your project's specific needs by creating custom rules. Define rules
   for variable naming conventions, code complexity thresholds, code style guidelines, and more.

- Detailed Reports:
   ``pysast`` generates comprehensive reports that highlight the violations found in your
   codebase. These reports (JSON) contain detailed information about the violating code snippets,
   allowing you to easily locate and rectify the identified issues.


Installation
------------

To install ``pysast``, you can use pip - the Python package installer. Simply run the following
command:

.. code-block:: shell

   pip install pysast

Once installed, you're ready to start using pysast for your code analysis needs.

Getting Started
---------------

Before you begin using ``pysast``, it's recommended to familiarize yourself with the package's
functionality and usage. The following sections will guide you through the essential steps to
set up ``pysast`` and run your first code scan:

1. :doc:`Rule Defintion <intro/sast_rules>`: Learn how to define rules in JSON or YAML format to specify the analysis criteria for your codebase.
2. :doc:`Running Scans <intro/sast_scans>`: Explore how to execute pysast to scan your files and generate detailed reports.
3. :doc:`Advanced Usage <api/index>`: Dive deeper into the advanced features and options offered by pysast to enhance your code analysis capabilities.

By following these steps, you'll be equipped with the knowledge and tools to effectively utilize
pysast in your projects.

.. note::
   For the latest updates, bug reports, or feature requests, please refer to the pysast GitHub
   repository: https://github.com/MatrixEditor/pysast. Feel free to contribute.

.. toctree::
   :hidden:
   :maxdepth: 3
   :caption: Getting Started

   intro/sast_rules
   intro/sast_scans

.. toctree::
   :hidden:
   :maxdepth: 3
   :caption: SAST API

   api/index

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
