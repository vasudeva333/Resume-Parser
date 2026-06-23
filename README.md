# Resume-Parser

INTERN ID: CITS5352

NAME: VASUDEVA REDDY

NO.OF WEEKS: 4

PROJECT NAME :Email-Spam-Classifier

PROJECT SCOPE:

A lightweight Python script that automatically parses PDF resumes to extract essential candidate details. It uses regular expressions and text matching to find contact information, technical skills, and project titles.

source code:

import PyPDF2, re


with open("VASUDEV.pdf", "rb") as f:
    text = "".join(p.extract_text() for p in PyPDF2.PdfReader(f).pages if p.extract_text())


email = re.findall(r"[\w.%+-]+@[\w.-]+\.[a-zA-Z]{2,}", text)
phone = re.findall(r"\b\d{10}\b", text)


skills = ["Python", "Java", "C", "C++", "SQL", "Machine Learning", "Deep Learning", "HTML", "CSS", "JavaScript", "React", "Data Science"]
found_skills = [s for s in skills if s.lower() in text.lower()]


p_match = re.search(r"Projects(.*?)(Education|Skills|Experience|Certifications|$)", text, re.I | re.S)
projects = [l.strip() for l in p_match.group(1).split("\n") if l.strip() and len(l.split()) <= 6] if p_match else []


print(f"Email: {email[0] if email else 'Not Found'}")
print(f"Phone: {phone[0] if phone else 'Not Found'}")
print(f"Skills: {found_skills}")
print(f"Projects: {projects}")



