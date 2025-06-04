# Courses System Setup Guide

This guide explains how to set up and use the new courses system in your Shopify theme using metaobjects.

## Overview

The courses system allows you to:
- Display courses using a custom metaobject (not products)
- Show courses in a featured section on any page
- Create individual course pages with full descriptions
- Maintain a courses listing page

## Setup Instructions

### 1. Create the Metaobject Definition

In your Shopify admin:

1. Go to **Settings** → **Custom data** → **Metaobjects**
2. Click **"Add definition"**
3. Set up the metaobject with these details:
   - **Name**: `Courses`
   - **Type**: `forlob` (this must match exactly)
   - **Access**: Choose appropriate access settings

### 2. Add Fields to the Metaobject

Add these fields to your `forlob` metaobject definition:

| Field Name | Type | Required | Description |
|------------|------|----------|-------------|
| `title` | Single line text | Yes | Course title |
| `description` | Rich text | Yes | Full course description (supports HTML) |
| `small_description` | Rich text | No | Short description for course cards |
| `primary_image` | File | No | Course featured image |
| `handle` | Single line text | Yes | URL-friendly course identifier |

### 3. Create Course Entries

1. In your Shopify admin, go to **Content** → **Metaobjects**
2. Select your **Courses** metaobject
3. Click **"Add entry"**
4. Fill in the course details:
   - **Title**: The course name
   - **Description**: Full course description with formatting
   - **Small Description**: Short description for course cards (optional)
   - **Primary Image**: Upload a featured image
   - **Handle**: URL-friendly identifier (e.g., "beginner-yoga")

### 4. Set Up Pages

#### Main Courses Page
1. Create a page with handle `courses`
2. Use the template `page.courses`
3. This will automatically display all your courses

#### Individual Course Pages
- Individual course pages are automatically created at URLs like:
  - `/pages/course-[handle]` (e.g., `/pages/course-beginner-yoga`)
- These use the template `page.course`
- No manual page creation needed - they're generated from the metaobject data

## Using the Sections

### Featured Courses Section

Add the **Featured Courses** section to any page/template:

**Settings available:**
- Heading text and size
- Number of courses to show (2-12)
- Number of columns on desktop (1-5)
- Show/hide featured images
- Show/hide "View all" button
- Custom "View all" button URL
- Color scheme
- Section padding

### Course Content Section

This section is automatically included in individual course pages and displays:
- Course featured image (from `primary_image` field)
- Course title
- Full course description (from `description` field)
- Back to courses button

## File Structure

The courses system includes these files:

```
sections/
├── featured-courses.liquid      # Featured courses section
├── course-content.liquid        # Individual course page content
└── courses-list.liquid         # All courses listing

snippets/
└── course-card.liquid          # Course card component

templates/
├── page.courses.json           # Main courses page template
└── page.course.json            # Individual course page template

assets/
├── section-featured-courses.css
├── section-course-content.css
└── section-courses-list.css
```

## Field Mapping

The system uses these metaobject fields:

- **Course Cards**: `primary_image`, `title`, `small_description`
- **Individual Course Pages**: `primary_image`, `title`, `description` (full)
- **URLs**: Generated from `handle` field

## Customization

### Styling
- Course cards inherit the blog card styling from your theme
- Customize the CSS files in the `assets/` folder to match your design
- Button styling uses the existing theme button styles

### URL Structure
- Main courses page: `/pages/courses`
- Individual courses: `/pages/course-[handle]`
- You can customize the URL pattern by modifying the `course_url` assignment in `snippets/course-card.liquid`

### Content Fields
To add more fields to courses:
1. Add the field to your metaobject definition in Shopify admin
2. Update the relevant Liquid files to display the new field
3. Add any necessary styling

## Troubleshooting

### Courses Not Appearing
1. Verify the metaobject type is exactly `forlob`
2. Check that courses have all required fields filled
3. Ensure the metaobject has proper access permissions

### Images Not Showing
1. Verify the field name is `primary_image` in your metaobject
2. Check that images are uploaded to the `primary_image` field
3. Ensure images have proper file permissions

### Individual Course Pages Not Working
1. Verify the page handle matches the pattern `course-[course-handle]`
2. Check that the course handle exists in your metaobject entries
3. Ensure the `page.course.json` template is being used

### Styling Issues
1. Check that all CSS files are properly linked
2. Verify the theme's blog card styles are working
3. Clear browser cache and theme cache

## Support

This courses system integrates with your existing theme styles and follows Shopify's best practices for performance and accessibility. 