---
layout: page
title: Projects
permalink: /Projects/
---
# Software
  <div data-iframe-width="150" data-iframe-height="270" data-share-badge-id="607113dc-2e1c-4eda-b865-149b83378a5b"></div>
  <script type="text/javascript">
    (function() {
      var s = document.createElement('script');
      s.type = 'text/javascript';
      s.async = true;
      s.src = '//cdn.youracclaim.com/assets/utilities/embed.js';
      var o = document.getElementsByTagName('script')[0];
      o.parentNode.insertBefore(s, o);
      })();
  </script>

##### [Redox OS](https://redox-os.org)
Redox is a microkernel-based operating system written in Rust. I am currently involved in a lot of ACPI work, specifically developing an AML interpreter for use within the kernel, and to develop a driver for the High Precision Event Timer (HPET), as defined in a document referenced by the ACPI specification.

AML is a bytecode in the ACPI specification, which contains a lot of important details on how the machine runs - it contains certain values needed to power the machine down, for example, and control methods for operating a lot of the machine hardware. This needs to be parsed, and then intercepted, to achieve a lot of important administration tasks, and due to the design of the spec, a recursive descent, multi-pass parser is required, in kernel mode.

##### [Patient Panic](https://github.com/CWood1/chimed)
A project completed as part of a team, for a competition while at university. I did the bulk of the programming, though the design itself was not mine. The intention behind the competition, and the design space we were operating in, was to design a game to call attention to blame culture, and to prompt people to think deeper about the assumptions they make.

##### Compiler
As part of my university education, I am writing a toy compiler in Haskell, for a toy language based loosely on Rust. Once this has been accepted by the university, to avoid possible claims of plagiarism, I intend to develop this as an open source application, to be compatible with the Rust compiler.

# Languages
I am currently working on learning Greek, though I am currently only at beginner level. I also have a beginner understanding of Mandarin and Spanish. Overall, I wish to learn, to at least B2 or C1 level, the following:

 - Greek
 - Mandarin Chinese
 - Esperanto
 - Arabic
 - Tamil
 - German
 - Russian
 - Korean
 - Japanese
 - Spanish