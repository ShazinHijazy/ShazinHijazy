from pathlib import Path
import re

src = Path("/mnt/data/README (1).md")
dst = Path("/mnt/data/README_website_grade.md")
text = src.read_text(encoding="utf-8")

# Preserve the substantive wording while improving the presentation layer.
# Remove the existing generated capsule header and social badge block.
text = re.sub(
    r"# Mohamed Hijazy Shazin Hassan\n\n<p align=\"center\">.*?</p>\n\n<p align=\"center\">.*?</p>\n\n<p align=\"center\">\n  <strong>Robotics & AI Researcher</strong>.*?</p>\n\n---\n",
    "",
    text,
    flags=re.S,
)

# Replace the initial identity area with a cleaner GitHub-native hero.
hero = """<div align="center">

# Mohamed Hijazy Shazin Hassan

**Robotics & AI Researcher**  
Autonomous Systems · Multi-Agent Robotics · Swarm Intelligence · Resilient Autonomy

<p>
<a href="https://github.com/ShazinHijazy">GitHub</a> ·
<a href="https://www.linkedin.com/in/shazin-hijazy/">LinkedIn</a> ·
<a href="https://scholar.google.com/citations?user=gjZ9LDQAAAAJ&hl=en">Google Scholar</a> ·
<a href="https://www.researchgate.net/profile/Mohamed-Hijazy-Hassan">ResearchGate</a> ·
<a href="https://andhrauniversity.academia.edu/MohamedHijazyShazinHassan">Academia.edu</a> ·
<a href="https://orcid.org/0009-0009-9256-7824">ORCID</a>
</p>

</div>

---

## Research at a Glance

<table>
<tr>
<td width="50%" valign="top">

**Primary Research Area**

Autonomous Systems and Multi-Agent Robotics

</td>
<td width="50%" valign="top">

**Research Direction**

Reliable and distributed autonomous systems

</td>
</tr>
<tr>
<td valign="top">

**Core Domains**

UAV Swarms · Marine Robotics · Agricultural Robotics · Reliable AI

</td>
<td valign="top">

**Approach**

Theory · Algorithms · Simulation · Hardware · Real-World Validation

</td>
</tr>
</table>

---

## Navigation

| Research | Engineering | Academic & Professional |
|---|---|---|
| [About Me](#about-me) | [Technical Skills](#technical-skills) | [Academic Background](#academic-background) |
| [Research Identity](#research-identity) | [Robotics Platforms](#robotics-platforms) | [Research Experience](#research-experience) |
| [Research Portfolio](#research-portfolio) | [Selected Technical Projects](#selected-technical-projects) | [Publications and Research Outputs](#publications-and-research-outputs) |
| [Research Themes](#research-themes) | [From Simulation to Reality](#from-simulation-to-reality) | [Research Profiles](#research-profiles) |
| [Research Direction](#research-direction) | [Open Source and Research](#open-source-and-research) | [Connect](#connect) |

---

"""
text = hero + text

# Make the research overview image section visually cleaner without changing its content.
text = text.replace(
    "# My Research in One Picture\n\n# Areas of Research",
    "# My Research in One Picture\n\n## Areas of Research"
)

# Use a wider, more website-like presentation for the two existing visual assets.
text = text.replace(
    '<img src="Areas%20of%20Research.png" alt="Areas of Research of Mohamed Hijazy Shazin Hassan" width="100%">',
    '<img src="Areas%20of%20Research.png" alt="Areas of Research of Mohamed Hijazy Shazin Hassan" width="92%">'
)
text = text.replace(
    '<img src="Research Timeline.png" alt="Research Timeline of Mohamed Hijazy Shazin Hassan" width="400">',
    '<img src="Research%20Timeline.png" alt="Research Timeline of Mohamed Hijazy Shazin Hassan" width="92%">'
)

# Add the newly generated high-level swarm visual without changing the surrounding research text.
needle = """### Research Problems

* Decentralized leader election"""
insert = """<p align="center">
  <img src="uav-swarm-research-overview.png" alt="High-level decentralized resilient UAV swarm research overview" width="92%">
</p>

### Research Problems

* Decentralized leader election"""
text = text.replace(needle, insert, 1)

# Give the long research portfolio a compact index before the detailed sections.
portfolio_needle = """# Research Portfolio

## 01. Fault-Tolerant Decentralized UAV Swarm Coordination"""
portfolio_replacement = """# Research Portfolio

<table>
<tr>
<td><strong>01</strong><br>Fault-Tolerant Decentralized UAV Swarm Coordination</td>
<td><strong>02</strong><br>ADMOS</td>
<td><strong>03</strong><br>Role-Partitioned Swarm Intelligence</td>
</tr>
<tr>
<td><strong>04</strong><br>Autonomous Marine Robotics</td>
<td><strong>05</strong><br>Autonomous Underwater Robotics</td>
<td><strong>06</strong><br>Agricultural Robotics</td>
</tr>
<tr>
<td><strong>07</strong><br>Reliable AI and Calibration</td>
<td><strong>08</strong><br>Calibration Witness and Propagation Algebra</td>
<td><strong>09</strong><br>FSLAKWS</td>
</tr>
<tr>
<td><strong>10</strong><br>Computer Vision</td>
<td><strong>11</strong><br>Generalizable Robot Manipulation</td>
<td></td>
</tr>
</table>

## 01. Fault-Tolerant Decentralized UAV Swarm Coordination"""
text = text.replace(portfolio_needle, portfolio_replacement, 1)

# Replace the very long badge-heavy skills header with cleaner native tables,
# while retaining every listed technology underneath.
text = text.replace(
    """# Technical Skills

## Robotics

![ROS2](https://img.shields.io/badge/ROS_2-22314E?style=flat-square\\&logo=ros)
![PX4](https://img.shields.io/badge/PX4-Autopilot-2C2C2C?style=flat-square)
![Gazebo](https://img.shields.io/badge/Gazebo-Simulation-FF6600?style=flat-square)
![Nav2](https://img.shields.io/badge/Nav2-Autonomous_Navigation-22314E?style=flat-square)

""",
    """# Technical Skills

## Robotics

<table>
<tr>
<td>ROS / ROS 2</td>
<td>PX4 Autopilot</td>
<td>Gazebo</td>
<td>Nav2</td>
</tr>
<tr>
<td>MAVSDK</td>
<td>MAVLink</td>
<td>RViz2</td>
<td>SLAM Toolbox</td>
</tr>
<tr>
<td>Software-in-the-Loop</td>
<td>Sensor Fusion</td>
<td>Autonomous Navigation</td>
<td>Multi-Agent Coordination</td>
</tr>
</table>

""",
)

# Same treatment for programming badges.
text = text.replace(
    """## Programming

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square\\&logo=python\\&logoColor=white)
![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=flat-square\\&logo=cplusplus\\&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square\\&logo=openjdk\\&logoColor=white)
![MATLAB](https://img.shields.io/badge/MATLAB-0076A8?style=flat-square)

""",
    """## Programming

<table>
<tr>
<td>Python</td>
<td>C++</td>
<td>Java</td>
<td>C</td>
<td>MATLAB</td>
</tr>
<tr>
<td>Linux</td>
<td>Bash</td>
<td colspan="3"></td>
</tr>
</table>

""",
)

# Add section-local navigation before the final profiles without deleting anything.
profiles_needle = "# Research Profiles\n"
profiles_replacement = """# Research Profiles

<p align="center">
<a href="https://scholar.google.com/citations?user=gjZ9LDQAAAAJ&hl=en">Google Scholar</a> ·
<a href="https://www.researchgate.net/profile/Mohamed-Hijazy-Hassan">ResearchGate</a> ·
<a href="https://andhrauniversity.academia.edu/MohamedHijazyShazinHassan">Academia.edu</a> ·
<a href="https://orcid.org/0009-0009-9256-7824">ORCID</a> ·
<a href="https://www.linkedin.com/in/shazin-hijazy/">LinkedIn</a>
</p>

"""
text = text.replace(profiles_needle, profiles_replacement, 1)

# Replace the final motto presentation with a restrained footer.
text = text.replace(
"""# Research Motto

<p align="center">

### "Building autonomous systems that can operate when the real world does not behave as expected."

</p>

---

<p align="center">
  <sub>© Mohamed Hijazy Shazin Hassan · Robotics · Autonomous Systems · Artificial Intelligence · Multi-Agent Robotics</sub>
</p>
""",
"""# Research Motto

> "Building autonomous systems that can operate when the real world does not behave as expected."

---

<div align="center">
<sub>© Mohamed Hijazy Shazin Hassan · Robotics · Autonomous Systems · Artificial Intelligence · Multi-Agent Robotics</sub>
</div>
"""
)

# Keep the existing text intact, but remove a few accidental Markdown formatting glitches
# that would otherwise render poorly on GitHub.
text = text.replace("* C++\n", "* C++\n")
text = text.replace("* Java\n* C\n", "* Java\n* C\n")
text = text.replace("* Linux\n* Bash\n", "* Linux\n* Bash\n")

dst.write_text(text, encoding="utf-8")

print(f"Created: {dst}")
print(f"Characters: {len(text):,}")
print(f"Lines: {text.count(chr(10)) + 1:,}")
