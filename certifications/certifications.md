---
layout: wrapper
title: Certifications
description: A collection of my professional certifications and training courses, demonstrating expertise across software development, cloud & data analytics, engineering tools, and professional/business skills.
main-image: /certificates-banner.png
permalink: /certifications/
---

<!--
  =====================================================================
  Certifications Page Template
  ---------------------------------------------------------------------
  This page uses:
    - A Quick Search Bar to filter certifications by text.
    - An Active Filters area that shows the currently selected skill tags.
    - Collapsible accordion sections (<details>) for grouping certifications by category.
    - Certification cards (<div class="cert-card">) with metadata and clickable skill tags.
    - JavaScript functions to add/remove filters and filter certification cards.
    - CSS styling for consistency and visual feedback.
  
  To add a new certification:
    1. Copy one of the <div class="cert-card"> blocks.
    2. Update the title, issued date, issuer, and credential link.
    3. Add appropriate <span class="skill-tag"> elements inside the Skills paragraph.
    4. Ensure the "data-skills" attribute includes a comma-separated list of tags.
  
  To add a new group, copy a <details class="cert-accordion"> section.
  =====================================================================
-->

<style>
  /* Quick Search Bar Styling */
  .cert-search {
    width: 100%;
    padding: 0.8rem;
    margin-bottom: 0.5rem;
    font-size: 1.1rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  /* Active Filters Container */
  #activeFilters {
    margin-bottom: 1rem;
  }
  .active-filter {
    display: inline-block;
    background: #007bff;
    color: #fff;
    padding: 0.3rem 0.6rem;
    margin: 0.2rem;
    border-radius: 4px;
    font-size: 0.9rem;
  }
  .active-filter .remove-btn {
    margin-left: 0.5rem;
    cursor: pointer;
    font-weight: bold;
  }
  /* Accordion Styling for Groups */
  .cert-accordion summary {
    cursor: pointer;
    font-size: 1.5rem;
    font-weight: bold;
    margin: 1rem 0;
    padding: 0.5rem;
    background: #f7f7f7;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  /* Certification Card Styling */
  .cert-card {
    border: 1px solid #ddd;
    padding: 1rem;
    margin: 1rem 0;
    border-radius: 4px;
    background: #fff;
  }
  .cert-card h3 { margin-top: 0; }
  /* Skill Tag Styling */
  .skill-tag {
    display: inline-block;
    background: #007bff;
    color: #fff;
    padding: 0.2rem 0.6rem;
    margin: 0.2rem;
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.9rem;
  }
  /* Visual Feedback: When pressed, a tag turns darker blue */
  .skill-tag:active {
    background: rgb(0, 29, 59);
  }
  /* Button Styling */
  .btn {
    display: inline-block;
    padding: 0.5rem 1rem;
    background: #28a745;
    color: #fff;
    text-decoration: none;
    border-radius: 4px;
    font-size: 0.9rem;
    margin-top: 0.5rem;
  }
</style>

<script>
  // Global active filters array
  var activeFilters = [];

  // Update the Active Filters UI
  function updateActiveFiltersUI() {
    var container = document.getElementById('activeFilters');
    container.innerHTML = '';
    activeFilters.forEach(function(filter) {
      var span = document.createElement('span');
      span.className = 'active-filter';
      span.innerText = filter;
      
      // Create a remove button for the active filter
      var removeBtn = document.createElement('span');
      removeBtn.className = 'remove-btn';
      removeBtn.innerText = ' x';
      removeBtn.onclick = function() {
        removeFilter(filter);
      };
      
      span.appendChild(removeBtn);
      container.appendChild(span);
    });
  }

  // Add a filter if not already present
  function addFilter(skill) {
    if (!activeFilters.includes(skill)) {
      activeFilters.push(skill);
      updateActiveFiltersUI();
      filterCertifications();
    }
  }

  // Remove a filter from the active filters array
  function removeFilter(skill) {
    activeFilters = activeFilters.filter(function(f) { return f !== skill; });
    updateActiveFiltersUI();
    filterCertifications();
  }

  // Filter certification cards based on search query and active filters
  function filterCertifications() {
    var query = document.getElementById('certSearch').value.toLowerCase();
    var cards = document.querySelectorAll('.cert-card');
    cards.forEach(function(card) {
      var cardText = card.innerText.toLowerCase();
      var matchesQuery = cardText.indexOf(query) > -1;
      var matchesFilters = activeFilters.every(function(filter) {
        return card.dataset.skills.toLowerCase().includes(filter.toLowerCase());
      });
      if (matchesQuery && matchesFilters) {
        card.style.display = "";
      } else {
        card.style.display = "none";
      }
    });
  }

  // Called when a skill tag is clicked
  function filterSkill(skill) {
    addFilter(skill);
  }
</script>

<!-- Quick Search/Filter Bar -->
<input type="text" id="certSearch" class="cert-search" placeholder="Search certifications..." onkeyup="filterCertifications()">
<div id="activeFilters"></div>

# Certifications & Licenses

Below are my certifications, grouped into four categories for easier navigation. Click on a category to expand or collapse, use the search bar above to filter, or click on a skill tag to add a filter.

---

<!-- ============================ Group 1: Software Development & Programming Certifications ============================ -->
<details class="cert-accordion" open>
  <summary>Group 1: Software Development & Programming Certifications</summary>
  
  <!-- 1. Apache Airflow Essential Training -->
  <div class="cert-card" data-skills="Apache Airflow, Python">
    <h3>Apache Airflow Essential Training</h3>
    <p><strong>Issued:</strong> Feb 2025</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Apache Airflow')">Apache Airflow</span>,
      <span class="skill-tag" onclick="filterSkill('Python')">Python</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/693c38e28bebeaefc50154850c9a3a7a53630b405e414e629088dcbdab5c1037?u=2075980" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 2. Building a Personal Portfolio with Django -->
  <div class="cert-card" data-skills="Django, Python">
    <h3>Building a Personal Portfolio with Django</h3>
    <p><strong>Issued:</strong> Jan 2025</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Django')">Django</span>,
      <span class="skill-tag" onclick="filterSkill('Python')">Python</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/e389800d27946ea74a1e3487de272c5f8c20d0ee2be785eac18d1b1b556f17d8" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 3. Elasticsearch Essential Training -->
  <div class="cert-card" data-skills="Elasticsearch, Data Analysis">
    <h3>Elasticsearch Essential Training</h3>
    <p><strong>Issued:</strong> Jan 2025</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Elasticsearch')">Elasticsearch</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/0dd4fa4c7f3111b7c762a6241f1a79caaef7245258e81fcabe129aa3aa3d79de" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 4. Elasticsearch in Depth -->
  <div class="cert-card" data-skills="Elasticsearch">
    <h3>Elasticsearch in Depth</h3>
    <p><strong>Issued:</strong> Jan 2025</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Elasticsearch')">Elasticsearch</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/95df3b214f11ddd6309363ee964938fbc4516f1f320084bfcceaf29efe41adbe" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 5. Learning Apache Airflow -->
  <div class="cert-card" data-skills="Apache Airflow, IT Automation, Python">
    <h3>Learning Apache Airflow</h3>
    <p><strong>Issued:</strong> Jan 2025</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Apache Airflow')">Apache Airflow</span>,
      <span class="skill-tag" onclick="filterSkill('IT Automation')">IT Automation</span>,
      <span class="skill-tag" onclick="filterSkill('Python')">Python</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/66d73c2973855db89c7cec52da1562a5bf818e4fedbc6218f73c9810f87d2276" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 6. Advanced Python: Working with Databases -->
  <div class="cert-card" data-skills="Python, Databases, SQL">
    <h3>Advanced Python: Working with Databases</h3>
    <p><strong>Issued:</strong> Dec 2024</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Python')">Python</span>,
      <span class="skill-tag" onclick="filterSkill('Databases')">Databases</span>,
      <span class="skill-tag" onclick="filterSkill('SQL')">SQL</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/9f63811960ea1b2858d1389273114c1f8029512f1f8d0bf52d9fdf578e175eb0" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 7. Deploying Django Apps: Make Your Site Go Live -->
  <div class="cert-card" data-skills="Django, Python">
    <h3>Deploying Django Apps: Make Your Site Go Live</h3>
    <p><strong>Issued:</strong> Dec 2024</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Django')">Django</span>,
      <span class="skill-tag" onclick="filterSkill('Python')">Python</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/992bf2d1a6dab7496c9dcc12d380318ab37b1e358ddcfc892ca18e210d989488" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 8. Django: Forms -->
  <div class="cert-card" data-skills="Django, Forms, Python">
    <h3>Django: Forms</h3>
    <p><strong>Issued:</strong> Dec 2024</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Django')">Django</span>,
      <span class="skill-tag" onclick="filterSkill('Forms')">Forms</span>,
      <span class="skill-tag" onclick="filterSkill('Python')">Python</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/832473ff86d2fc6907e398320d8a5f21016352f6fd35873fdeeda0ad2fcb9508" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 9. Docker for Developers -->
  <div class="cert-card" data-skills="Docker">
    <h3>Docker for Developers</h3>
    <p><strong>Issued:</strong> Dec 2024</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Docker')">Docker</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/cc48bfc0f3a777d9358ff9f49913296c5960a3d90f10ac8d3500ead44e5c9126" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 10. Flask Essential Training (2019) -->
  <div class="cert-card" data-skills="Flask, Python">
    <h3>Flask Essential Training (2019)</h3>
    <p><strong>Issued:</strong> Dec 2024</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Flask')">Flask</span>,
      <span class="skill-tag" onclick="filterSkill('Python')">Python</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/d21fac44501f89f9453c87f0073b911c5cc2fc340c60827d88a63fdd47b779c4" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 11. Python Parallel and Concurrent Programming Part 1 -->
  <div class="cert-card" data-skills="Python, Concurrent Programming, Parallel Computing">
    <h3>Python Parallel and Concurrent Programming Part 1</h3>
    <p><strong>Issued:</strong> Dec 2024</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Python')">Python</span>,
      <span class="skill-tag" onclick="filterSkill('Concurrent Programming')">Concurrent Programming</span>,
      <span class="skill-tag" onclick="filterSkill('Parallel Computing')">Parallel Computing</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/d04deca19b34b8709f2291bfed855a3ecaebfac9e1c87008b750310625c22705" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 12. Practical GitHub Actions -->
  <div class="cert-card" data-skills="GitHub, Git">
    <h3>Practical GitHub Actions</h3>
    <p><strong>Issued:</strong> Nov 2023</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('GitHub')">GitHub</span>,
      <span class="skill-tag" onclick="filterSkill('Git')">Git</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/212afbb66f923b27c85cc4fb214022fd5d1c1d1415632e390b21e5f71aface2f" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 13. Practical GitHub Code Search -->
  <div class="cert-card" data-skills="GitHub, Git">
    <h3>Practical GitHub Code Search</h3>
    <p><strong>Issued:</strong> Nov 2023</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('GitHub')">GitHub</span>,
      <span class="skill-tag" onclick="filterSkill('Git')">Git</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/5dfac62a378373b6fd261c8d7df64c95449f240372cb8c5a87cc65fc51e0f9ae" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 14. Practical GitHub Copilot -->
  <div class="cert-card" data-skills="GitHub Copilot">
    <h3>Practical GitHub Copilot</h3>
    <p><strong>Issued:</strong> Nov 2023</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('GitHub Copilot')">GitHub Copilot</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/a10f461959fe3efc5fce0e9b9f9bc8fbb913fcf106db1c44ae64efad1b07f805" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 15. Practical GitHub Project Management and Collaboration -->
  <div class="cert-card" data-skills="GitHub, Project Management">
    <h3>Practical GitHub Project Management and Collaboration</h3>
    <p><strong>Issued:</strong> Nov 2023</p>
    <p><strong>Issued by:</strong> LinkedIn</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('GitHub')">GitHub</span>,
      <span class="skill-tag" onclick="filterSkill('Project Management')">Project Management</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/1c2dc7ed5f811e4faff27dfaf39e55174286c9d6fdcb66a34c8c165d67ffcfba" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 16. Career Essentials in Software Development by Microsoft and LinkedIn -->
  <div class="cert-card" data-skills="Software Development, Programming">
    <h3>Career Essentials in Software Development by Microsoft and LinkedIn</h3>
    <p><strong>Issued:</strong> Oct 2023</p>
    <p><strong>Issued by:</strong> Microsoft</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Software Development')">Software Development</span>,
      <span class="skill-tag" onclick="filterSkill('Programming')">Programming</span>
    </p>
    <a href="https://www.linkedin.com/learning/certificates/e95d35618fc2869cdbe955bd231ee8814da2aa71b6330b3d5dbf1d3d7bc7f285" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 17. Basic Python Programming for Business -->
  <div class="cert-card" data-skills="Business Analysis, Python">
    <h3>Basic Python Programming for Business</h3>
    <p><strong>Issued:</strong> Jul 2023</p>
    <p><strong>Issued by:</strong> Arizona State University</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Business Analysis')">Business Analysis</span>,
      <span class="skill-tag" onclick="filterSkill('Python')">Python</span>
    </p>
    <a href="https://drive.google.com/file/d/1dPuXyEDMi9ZUUfSHw4-sh-XxG6jq6LQF/view?usp=sharing" target="_blank" class="btn">Show Credential</a>
  </div>
  
</details>

---

<!-- ============================ Group 2: Cloud, Data & Analytics Certifications ============================ -->
<details class="cert-accordion" open>
  <summary>Group 2: Cloud, Data & Analytics Certifications</summary>
  
  <!-- 1. AWS Educate: Getting Started with Cloud Ops -->
  <div class="cert-card" data-skills="AWS, Cloud Operations">
    <h3>AWS Educate: Getting Started with Cloud Ops</h3>
    <p><strong>Issued:</strong> Nov 2024</p>
    <p><strong>Issued by:</strong> Amazon Web Services (AWS)</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('AWS')">AWS</span>,
      <span class="skill-tag" onclick="filterSkill('Cloud Operations')">Cloud Operations</span>
    </p>
    <a href="https://www.credly.com/badges/b95e8499-0bf8-4fe5-8b44-6ba3088f67dd/linked_in_profile" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 2. AWS Educate: Getting Started with Compute -->
  <div class="cert-card" data-skills="AWS">
    <h3>AWS Educate: Getting Started with Compute</h3>
    <p><strong>Issued:</strong> Nov 2024</p>
    <p><strong>Issued by:</strong> Amazon Web Services (AWS)</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('AWS')">AWS</span></p>
    <a href="https://www.credly.com/badges/43eaeeb6-0eb5-4835-8133-9e328a8b46b0/linked_in_profile" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 3. AWS Educate: Getting Started with Databases -->
  <div class="cert-card" data-skills="AWS, Databases">
    <h3>AWS Educate: Getting Started with Databases</h3>
    <p><strong>Issued:</strong> Nov 2024</p>
    <p><strong>Issued by:</strong> Amazon Web Services (AWS)</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('AWS')">AWS</span>,
      <span class="skill-tag" onclick="filterSkill('Databases')">Databases</span>
    </p>
    <a href="https://www.credly.com/badges/db940bb7-931b-490c-98de-03d91e54b5fe/linked_in_profile" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 4. AWS Educate: Getting Started with Networking -->
  <div class="cert-card" data-skills="AWS, Networking">
    <h3>AWS Educate: Getting Started with Networking</h3>
    <p><strong>Issued:</strong> Nov 2024</p>
    <p><strong>Issued by:</strong> Amazon Web Services (AWS)</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('AWS')">AWS</span>,
      <span class="skill-tag" onclick="filterSkill('Networking')">Networking</span>
    </p>
    <a href="https://www.credly.com/badges/095a7be8-ad6b-4083-a079-cb6897ed2cf3/linked_in_profile" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 5. AWS Educate: Getting Started with Security -->
  <div class="cert-card" data-skills="AWS, Security">
    <h3>AWS Educate: Getting Started with Security</h3>
    <p><strong>Issued:</strong> Nov 2024</p>
    <p><strong>Issued by:</strong> Amazon Web Services (AWS)</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('AWS')">AWS</span>,
      <span class="skill-tag" onclick="filterSkill('Security')">Security</span>
    </p>
    <a href="https://www.credly.com/badges/3ac2f8f6-9d42-4ecc-a8c9-b6716da3ec46/linked_in_profile" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 6. AWS Educate: Getting Started with Serverless -->
  <div class="cert-card" data-skills="AWS, Serverless">
    <h3>AWS Educate: Getting Started with Serverless</h3>
    <p><strong>Issued:</strong> Nov 2024</p>
    <p><strong>Issued by:</strong> Amazon Web Services (AWS)</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('AWS')">AWS</span>,
      <span class="skill-tag" onclick="filterSkill('Serverless')">Serverless</span>
    </p>
    <a href="https://www.credly.com/badges/ea996072-47db-4f63-b048-554833ec7771/linked_in_profile" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 7. AWS Educate: Getting Started with Storage -->
  <div class="cert-card" data-skills="AWS, Storage">
    <h3>AWS Educate: Getting Started with Storage</h3>
    <p><strong>Issued:</strong> Nov 2024</p>
    <p><strong>Issued by:</strong> Amazon Web Services (AWS)</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('AWS')">AWS</span>,
      <span class="skill-tag" onclick="filterSkill('Storage')">Storage</span>
    </p>
    <a href="https://www.credly.com/badges/a0204007-a097-4159-b695-64d4cd4f2e54/linked_in_profile" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 8. M112: MongoDB Diagnostic Thinking -->
  <div class="cert-card" data-skills="MongoDB">
    <h3>M112: MongoDB Diagnostic Thinking</h3>
    <p><strong>Issued:</strong> Nov 2022</p>
    <p><strong>Issued by:</strong> MongoDB</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('MongoDB')">MongoDB</span></p>
    <a href="https://learn.mongodb.com/c/XeHGngo3Rm-8jbhX6y1tiw" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 9. Advance Python Packages for Business Analytics ASU -->
  <div class="cert-card" data-skills="Business Analysis, IT Business Analysis, Pandas, NumPy, Machine Learning, Data Visualization, Python">
    <h3>Advance Python Packages for Business Analytics ASU</h3>
    <p><strong>Issued:</strong> Jun 2024</p>
    <p><strong>Issued by:</strong> Arizona State University</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Business Analysis')">Business Analysis</span>,
      <span class="skill-tag" onclick="filterSkill('IT Business Analysis')">IT Business Analysis</span>,
      <span class="skill-tag" onclick="filterSkill('Pandas')">Pandas</span>,
      <span class="skill-tag" onclick="filterSkill('NumPy')">NumPy</span>,
      <span class="skill-tag" onclick="filterSkill('Machine Learning')">Machine Learning</span>,
      <span class="skill-tag" onclick="filterSkill('Data Visualization')">Data Visualization</span>,
      <span class="skill-tag" onclick="filterSkill('Python')">Python</span>
    </p>
    <a href="https://drive.google.com/file/d/1C_Tmts2uwiPoTbzj8Qbv2YCHqMI5WPLb/view?usp=sharing" target="_blank" class="btn">Download Certificate</a>
  </div>
  
  <!-- 10. Understanding Data Course ASU -->
  <div class="cert-card" data-skills="Data Analysis">
    <h3>Understanding Data Course ASU</h3>
    <p><strong>Issued:</strong> Jun 2024</p>
    <p><strong>Issued by:</strong> Arizona State University</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('Data Analysis')">Data Analysis</span></p>
    <a href="https://drive.google.com/file/d/1EW7EE4SlCFv8DL2_hrv6piiqLq5hOZvu/view?usp=sharing" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 11. HCIP-AI-EI Developer V2.0 Course -->
  <div class="cert-card" data-skills="Machine Learning">
    <h3>HCIP-AI-EI Developer V2.0 Course</h3>
    <p><strong>Issued:</strong> Oct 2023</p>
    <p><strong>Issued by:</strong> Huawei</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('Machine Learning')">Machine Learning</span></p>
    <a href="https://drive.google.com/file/d/1o27t2IAmBtZEnvVcl7i5d7aJkYFQx_P5/view?usp=sharing" target="_blank" class="btn">Show Credential</a>
  </div>
  
</details>

---

<!-- ============================ Group 3: Engineering, Technical Tools & Automation Certifications ============================ -->
<details class="cert-accordion" open>
  <summary>Group 3: Engineering, Technical Tools & Automation Certifications</summary>
  
  <!-- 1. Cybersecurity Fundamentals -->
  <div class="cert-card" data-skills="Cybersecurity, IBM">
    <h3>Cybersecurity Fundamentals</h3>
    <p><strong>Issued:</strong> Nov 2024</p>
    <p><strong>Issued by:</strong> IBM</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('Cybersecurity')">Cybersecurity</span></p>
    <a href="https://www.credly.com/badges/b42f7bf6-2c24-4fc2-a528-2b1e0179867c/linked_in_profile" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 2. Explore Emerging Tech -->
  <div class="cert-card" data-skills="Emerging Tech">
    <h3>Explore Emerging Tech</h3>
    <p><strong>Issued:</strong> Nov 2024</p>
    <p><strong>Issued by:</strong> IBM</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('Emerging Tech')">Emerging Tech</span></p>
    <a href="https://www.credly.com/badges/bc8e9dcf-0774-470a-91fd-55c56f9107a9/linked_in_profile" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 3. Working in a Digital World: Professional Skills -->
  <div class="cert-card" data-skills="Digital Transformation Initiatives">
    <h3>Working in a Digital World: Professional Skills</h3>
    <p><strong>Issued:</strong> Nov 2024</p>
    <p><strong>Issued by:</strong> IBM</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('Digital Transformation Initiatives')">Digital Transformation Initiatives</span></p>
    <a href="https://www.credly.com/badges/b67b2d61-6e9b-4ddb-8e31-8ad26a41b494/linked_in_profile" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 4. IBM ile Kodluyoruz: CyberStart -->
  <div class="cert-card" data-skills="Cybersecurity">
    <h3>IBM ile Kodluyoruz: CyberStart</h3>
    <p><strong>Issued:</strong> Dec 2024</p>
    <p><strong>Issued by:</strong> Kodluyoruz</p>
    <p><strong>Credential ID:</strong> 56851972550516</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('Cybersecurity')">Cybersecurity</span></p>
    <a href="https://verified.sertifier.com/tr/verify/56851972550516/" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 5. Microcontrollers with Arduino 3 -->
  <div class="cert-card" data-skills="Arduino, Microcontrollers">
    <h3>Microcontrollers with Arduino 3</h3>
    <p><strong>Issued:</strong> Mar 2024</p>
    <p><strong>Issued by:</strong> Orta Doğu Teknik Üniversitesi</p>
    <p><strong>Credential ID:</strong> 294b74c0-eace-11ee-8299-2f7354ae9e17</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Arduino')">Arduino</span>,
      <span class="skill-tag" onclick="filterSkill('Microcontrollers')">Microcontrollers</span>
    </p>
    <a href="https://bilgeis.net/moodle/mod/simplecertificate/verify.php?code=294b74c0-eace-11ee-8299-2f7354ae9e17" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 6. Raspberry Pi Advanced Level -->
  <div class="cert-card" data-skills="Raspberry Pi, Linux">
    <h3>Raspberry Pi Advanced Level</h3>
    <p><strong>Issued:</strong> Mar 2024</p>
    <p><strong>Issued by:</strong> Orta Doğu Teknik Üniversitesi</p>
    <p><strong>Credential ID:</strong> 70496490-eadb-11ee-8b05-e921ce248bf7</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Raspberry Pi')">Raspberry Pi</span>,
      <span class="skill-tag" onclick="filterSkill('Linux')">Linux</span>
    </p>
    <a href="https://bilgeis.net/moodle/mod/simplecertificate/verify.php?code=70496490-eadb-11ee-8b05-e921ce248bf7" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 7. Debugging in Studio -->
  <div class="cert-card" data-skills="Robotic Process Automation, RPA">
    <h3>Debugging in Studio</h3>
    <p><strong>Issued:</strong> Nov 2023</p>
    <p><strong>Issued by:</strong> UiPath</p>
    <p><strong>Credential ID:</strong> 11262023092929390</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Robotic Process Automation')">Robotic Process Automation (RPA)</span>
    </p>
    <a href="https://drive.google.com/file/d/163rqnNj444IfyFK-hzkE_wXOd6vwqUVm/view?usp=sharing" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 8. Foundational MATLAB -->
  <div class="cert-card" data-skills="MATLAB">
    <h3>Foundational MATLAB</h3>
    <p><strong>Issued:</strong> Nov 2023</p>
    <p><strong>Issued by:</strong> MathWorks</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('MATLAB')">MATLAB</span></p>
    <a href="https://www.credly.com/badges/c0c849d7-2cbe-49a1-93fe-79e67bede738/linked_in_profile" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 9. Simulink Fundamentals -->
  <div class="cert-card" data-skills="MATLAB, Simulink">
    <h3>Simulink Fundamentals</h3>
    <p><strong>Issued:</strong> Nov 2023</p>
    <p><strong>Issued by:</strong> MathWorks</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('MATLAB')">MATLAB</span>,
      <span class="skill-tag" onclick="filterSkill('Simulink')">Simulink</span>
    </p>
    <a href="https://matlabacademy.mathworks.com/progress/share/certificate.html?id=8bd3c708-6d1d-450b-882e-a5b3befb2e89&" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 10. UiPath RPA Developer FastStart -->
  <div class="cert-card" data-skills="Robotic Process Automation, UiPath">
    <h3>UiPath RPA Developer FastStart</h3>
    <p><strong>Issued:</strong> Nov 2023</p>
    <p><strong>Issued by:</strong> UiPath</p>
    <p><strong>Credential ID:</strong> 11302023145856811</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Robotic Process Automation')">Robotic Process Automation (RPA)</span>,
      <span class="skill-tag" onclick="filterSkill('UiPath')">UiPath</span>
    </p>
    <a href="https://drive.google.com/file/d/1L_YMSQSbHm5zMLF-thCPvHT8esKS79C2/view?usp=sharing" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 11. MATLAB Onramp -->
  <div class="cert-card" data-skills="MATLAB">
    <h3>MATLAB Onramp</h3>
    <p><strong>Issued:</strong> Oct 2023</p>
    <p><strong>Issued by:</strong> MATLAB Coding</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('MATLAB')">MATLAB</span></p>
    <a href="https://matlabacademy.mathworks.com/progress/share/certificate.html?id=267326c0-a755-4abb-adad-6c4d3cfaa9ee&" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 12. Machine Learning Project Success Planning -->
  <div class="cert-card" data-skills="Project Planning, Machine Learning">
    <h3>Machine Learning Project Success Planning</h3>
    <p><strong>Issued:</strong> Oct 2023</p>
    <p><strong>Issued by:</strong> HPE AI</p>
    <p><strong>Credential ID:</strong> f2dg7sbigm7b</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Project Planning')">Project Planning</span>,
      <span class="skill-tag" onclick="filterSkill('Machine Learning')">Machine Learning</span>
    </p>
    <a href="https://verify.skilljar.com/c/f2dg7sbigm7b" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 13. Beamline for Schools Cern Competition -->
  <div class="cert-card" data-skills="Engineering">
    <h3>Beamline for Schools Cern Competition</h3>
    <p><strong>Issued:</strong> Mar 2020</p>
    <p><strong>Issued by:</strong> Beamline for Schools (BL4S)</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('Engineering')">Engineering</span></p>
    <a href="https://www.linkedin.com/in/daglarduman/details/certifications/1739042592209/single-media-viewer?type=DOCUMENT&profileId=ACoAACWAci0BonVwJ6WHL5pZPhgbHOa_ymTdPDY&lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_certifications_details%3BcDvtoY2jRECDk%2BKUzYb0vw%3D%3D" target="_blank" class="btn">Show Credential</a>
  </div>
  
</details>

---

<!-- ============================ Group 4: Professional & Business Skills Certifications ============================ -->
<details class="cert-accordion" open>
  <summary>Group 4: Professional & Business Skills Certifications</summary>
  
  <!-- 1. SHGM / Sivil Havacılık Genel Müdürlüğü - IHA-0 - Sportif / Amatör -->
  <div class="cert-card" data-skills="Drone Piloting, UAV">
    <h3>SHGM / Sivil Havacılık Genel Müdürlüğü - IHA-0 - Sportif / Amatör</h3>
    <p><strong>Issued:</strong> Feb 2025</p>
    <p><strong>Credential ID:</strong> TR-IHA0H12003385</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Drone Piloting')">Drone Piloting</span>,
      <span class="skill-tag" onclick="filterSkill('UAV')">UAV</span>
    </p>
    <a href="https://www.linkedin.com/in/daglarduman/details/certifications/1740753965681/single-media-viewer?type=DOCUMENT&profileId=ACoAACWAci0BonVwJ6WHL5pZPhgbHOa_ymTdPDY&lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_certifications_details%3BcDvtoY2jRECDk%2BKUzYb0vw%3D%3D" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 2. Yapay Zeka İle Dönüştürelim Katılım Belgesi -->
  <div class="cert-card" data-skills="AI, Digital Transformation Initiatives">
    <h3>Yapay Zeka İle Dönüştürelim Katılım Belgesi</h3>
    <p><strong>Issued:</strong> Feb 2025</p>
    <p><strong>Issued by:</strong> Kodluyoruz</p>
    <p><strong>Credential ID:</strong> 07328994234280</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('AI')">AI</span>,
      <span class="skill-tag" onclick="filterSkill('Digital Transformation Initiatives')">Digital Transformation Initiatives</span>
    </p>
    <a href="https://verified.sertifier.com/en/verify/07328994234280/" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 3. Automotive Summer Camp -->
  <div class="cert-card" data-skills="Automotive, Engineering">
    <h3>Automotive Summer Camp</h3>
    <p><strong>Issued:</strong> Jul 2024</p>
    <p><strong>Issued by:</strong> OSD - Otomotiv Sanayii Derneği</p>
    <p><strong>Credential ID:</strong> OSDB00457B0</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Automotive')">Automotive</span>,
      <span class="skill-tag" onclick="filterSkill('Engineering')">Engineering</span>
    </p>
    <a href="https://dogrulama.ogrencikariyeri.com/images/documents/OSDB00457B0.jpg" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 4. Principles Programming Language ASU -->
  <div class="cert-card" data-skills="Syntax, Algorithms, Compiler Construction, Programming Languages">
    <h3>Principles Programming Language ASU</h3>
    <p><strong>Issued:</strong> Jun 2024</p>
    <p><strong>Issued by:</strong> Arizona State University</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Syntax')">Syntax</span>,
      <span class="skill-tag" onclick="filterSkill('Algorithms')">Algorithms</span>,
      <span class="skill-tag" onclick="filterSkill('Compiler Construction')">Compiler Construction</span>,
      <span class="skill-tag" onclick="filterSkill('Programming Languages')">Programming Languages</span>
    </p>
    <a href="https://drive.google.com/file/d/19KLXYmIyy5VxX6tSafJA_iauYRL-O93O/view?usp=sharing&usp=embed_facebook" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 5. Seninle İyi Gelecek Etkinliği Katılım Belgesi -->
  <div class="cert-card" data-skills="Startup Development, Startups">
    <h3>Seninle İyi Gelecek Etkinliği Katılım Belgesi</h3>
    <p><strong>Issued:</strong> May 2024</p>
    <p><strong>Issued by:</strong> Youthall</p>
    <p><strong>Credential ID:</strong> 33941495020193</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Startup Development')">Startup Development</span>,
      <span class="skill-tag" onclick="filterSkill('Startups')">Startups</span>
    </p>
    <a href="https://verified.sertifier.com/en/verify/33941495020193/" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 6. Linux Certificate -->
  <div class="cert-card" data-skills="Linux">
    <h3>Linux Certificate</h3>
    <p><strong>Issued:</strong> Apr 2024</p>
    <p><strong>Issued by:</strong> Chegg Inc.</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('Linux')">Linux</span></p>
    <a href="https://www.linkedin.com/in/daglarduman/details/certifications/1722512536666/single-media-viewer?type=IMAGE&profileId=ACoAACWAci0BonVwJ6WHL5pZPhgbHOa_ymTdPDY&lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_certifications_details%3BTlNtlHZVSECtGTrSUsmK0A%3D%3D" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 7. HP Life Certified for 3D Printing -->
  <div class="cert-card" data-skills="3D Printing, Hardware & Embedded Systems">
    <h3>HP Life Certified for 3D Printing</h3>
    <p><strong>Issued:</strong> Sep 2023</p>
    <p><strong>Issued by:</strong> HP LIFE</p>
    <p><strong>Credential ID:</strong> HPL-EN29</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('3D Printing')">3D Printing</span>,
      <span class="skill-tag" onclick="filterSkill('Hardware & Embedded Systems')">Hardware & Embedded Systems</span>
    </p>
    <a href="https://www.life-global.org/certificate/1ab11aa5-f12f-4eb1-a646-861e1ee2561c" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 8. HP Life Certified for Creating Effective Business Websites -->
  <div class="cert-card" data-skills="Business Analysis, Web Development & APIs">
    <h3>HP Life Certified for Creating Effective Business Websites</h3>
    <p><strong>Issued:</strong> Sep 2023</p>
    <p><strong>Issued by:</strong> HP LIFE</p>
    <p><strong>Credential ID:</strong> HPL-EN17</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Business Analysis')">Business Analysis</span>,
      <span class="skill-tag" onclick="filterSkill('Web Development & APIs')">Web Development & APIs</span>
    </p>
    <a href="https://www.life-global.org/certificate/1abf9665-d94f-44b7-9bc5-d4e7f3803b62" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 9. HP Life Certified for IT for Business Success -->
  <div class="cert-card" data-skills="Business Analysis, Project Management">
    <h3>HP Life Certified for IT for Business Success</h3>
    <p><strong>Issued:</strong> Sep 2023</p>
    <p><strong>Issued by:</strong> HP LIFE</p>
    <p><strong>Credential ID:</strong> HPL-EN24</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Business Analysis')">Business Analysis</span>,
      <span class="skill-tag" onclick="filterSkill('Project Management')">Project Management</span>
    </p>
    <a href="https://www.life-global.org/certificate/97bd00db-5781-4c20-addb-7518914709b9" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 10. HP Life Certified Social Media Marketing -->
  <div class="cert-card" data-skills="Business Analysis">
    <h3>HP Life Certified Social Media Marketing</h3>
    <p><strong>Issued:</strong> Dec 2022</p>
    <p><strong>Issued by:</strong> HP LIFE</p>
    <p><strong>Credential ID:</strong> HPL-EN02</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('Business Analysis')">Business Analysis</span></p>
    <a href="https://www.life-global.org/certificate/9d86e80a-a720-4650-b5ee-1a7a73dcd97f" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 11. HP Life Certified for Presenting Data -->
  <div class="cert-card" data-skills="Business Analysis, Data Analysis, Software Documentation, Data Visualization">
    <h3>HP Life Certified for Presenting Data</h3>
    <p><strong>Issued:</strong> Dec 2022</p>
    <p><strong>Issued by:</strong> HP LIFE</p>
    <p><strong>Credential ID:</strong> HPL-EN14</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Business Analysis')">Business Analysis</span>,
      <span class="skill-tag" onclick="filterSkill('Data Analysis')">Data Analysis</span>,
      <span class="skill-tag" onclick="filterSkill('Software Documentation')">Software Documentation</span>,
      <span class="skill-tag" onclick="filterSkill('Data Visualization')">Data Visualization</span>
    </p>
    <a href="https://www.life-global.org/certificate/60d38ace-271f-4580-b3ae-ec5b30d43764" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 12. ESP Skills Pass Certificate -->
  <div class="cert-card" data-skills="Entrepreneurship">
    <h3>ESP Skills Pass Certificate</h3>
    <p><strong>Issued by:</strong> Entrepreneurial Skills Pass (ESP)</p>
    <p><strong>Credential ID:</strong> ESP34000249</p>
    <p><strong>Skills:</strong> <span class="skill-tag" onclick="filterSkill('Entrepreneurship')">Entrepreneurship</span></p>
    <a href="https://drive.google.com/file/d/1aobTu844fHhedejuCLx1hW34RbNOwM9I/view?usp=sharing" target="_blank" class="btn">Show Credential</a>
  </div>
  
  <!-- 13. HCSA-Sales-IP Network V5.0 Certification -->
  <div class="cert-card" data-skills="Business Analysis, Computer Hardware Troubleshooting, Hardware Support">
    <h3>HCSA-Sales-IP Network V5.0 Certification</h3>
    <p><strong>Issued:</strong> Oct 2023</p>
    <p><strong>Issued by:</strong> Huawei</p>
    <p><strong>Skills:</strong> 
      <span class="skill-tag" onclick="filterSkill('Business Analysis')">Business Analysis</span>,
      <span class="skill-tag" onclick="filterSkill('Computer Hardware Troubleshooting')">Computer Hardware Troubleshooting</span>,
      <span class="skill-tag" onclick="filterSkill('Hardware Support')">Hardware Support</span>
    </p>
    <a href="https://drive.google.com/file/d/1K-8eXAJ20MNaFR-NnKPjvtO36GysuMeW/view?usp=sharing" target="_blank" class="btn">Show Credential</a>
  </div>
  
</details>

<!-- ============================ End of Group 4 ============================ -->

<!--
  =====================================================================
  End of Certifications Page Template
  ---------------------------------------------------------------------
  This template supports:
    - Dynamic filtering by search text and active skill tags.
    - Active filters display with removable "x" for each tag.
    - Collapsible accordion sections for different certification groups.
    - Consistent styling for skill tags and buttons.
  =====================================================================
-->
