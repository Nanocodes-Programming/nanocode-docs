# Team API Documentation

This documentation provides an overview of the Team API, which is used to manage and retrieve information about teams and their skills, certificates, and tags.

### Endpoints

#### 1. List Teams

- `GET /team/`: Retrieve a list of all teams.

##### Request

- No parameters are required for this endpoint.

##### Response

- Success: HTTP 200 OK with a list of all teams.
- Failure: HTTP 400 Bad Request with error message.

##### Example Response

```json
[
    {
        "id": 1,
        "name": "Team A",
        "image": "http://example.com/image.jpg",
        "years_of_experience": 5,
        "stack": "ui-ux",
        "educational_qualification": "Bachelor's Degree in UI/UX Design",
        "description": "We are a team of UI/UX designers.",
        "twitter_link": "http://twitter.com/team_a",
        "instagram_link": "http://instagram.com/team_a",
        "facebook_link": "http://facebook.com/team_a",
        "linkedln_link": "http://linkedin.com/team_a",
        "slug": "team-a",
        "email": "team_a@example.com"
    },
    // ... more teams
]
```

#### 2. Retrieve Team Details

- `GET /team/{id}/`: Retrieve details of a specific team.

##### Request

- `id`: The ID of the team.

##### Response

- Success: HTTP 200 OK with the details of the specified team.
- Failure: HTTP 404 Not Found if the team does not exist.

##### Example Response

```json
{
    "id": 1,
    "name": "Team A",
    "image": "http://example.com/image.jpg",
    "years_of_experience": 5,
    "stack": "ui-ux",
    "educational_qualification": "Bachelor's Degree in UI/UX Design",
    "description": "We are a team of UI/UX designers.",
    "twitter_link": "http://twitter.com/team_a",
    "instagram_link": "http://instagram.com/team_a",
    "facebook_link": "http://facebook.com/team_a",
    "linkedln_link": "http://linkedin.com/team_a",
    "slug": "team-a",
    "email": "team_a@example.com"
}
```

#### 3. Get Teams by Stack

- `GET /get_teams_by_stack/{stack}`: Retrieve a list of teams with a specific stack.

##### Request

- `stack`: The stack of the team.

##### Response

- Success: HTTP 200 OK with a list of teams with the specified stack.
- Failure: HTTP 404 Not Found if no teams with the specified stack exist.

##### Example Response

```json
[
    {
        "id": 1,
        "name": "Team A",
        "image": "http://example.com/image.jpg",
        "years_of_experience": 5,
        "stack": "ui-ux",
        "educational_qualification": "Bachelor's Degree in UI/UX Design",
        "description": "We are a team of UI/UX designers.",
        "twitter_link": "http://twitter.com/team_a",
        "instagram_link": "http://instagram.com/team_a",
        "facebook_link": "http://facebook.com/team_a",
        "linkedln_link": "http://linkedin.com/team_a",
        "slug": "team-a",
        "email": "team_a@example.com"
    },
    // ... more teams
]
```

### Permissions

- `TeamsViewSet`: Allows anyone to access.
- `GetTeamsByStackViewSet`: Allows anyone to access.
- `SkillViewSet`: Requires admin authentication for non-safe methods.
- `GetSkillByTeamViewSet`: Allows anyone to access.
- `CertificateViewSet`: Requires admin authentication for non-safe methods.
- `GetCertificatesByTeamViewSet`: Allows anyone to access.
- `GetTeamByTagViewSet`: Requires admin authentication for non-safe methods.

### URL Patterns

- `/team/`: Maps to the `TeamsViewSet` view.
- `/get_teams_by_stack/{stack}`: Maps to the `GetTeamsByStackViewSet` view.
- `/skill/`: Maps to the `SkillViewSet` view.
- `/get_skills_by_team/{team}`: Maps to the `GetSkillByTeamViewSet` view.
- `/certificate/`: Maps to the `CertificateViewSet` view.
- `/get_certificate_by_team/{team}`: Maps to the `GetCertificatesByTeamViewSet` view.
- `/get_team_by_tag/{tag_id}`: Maps to the `GetTeamByTagViewSet` view.

### Serializers

- `TeamSerializer`: Serializes the `Team` model.
- `SkillSerializer`: Serializes the `Skill` model.
- `CertificateSerializer`: Serializes the `Certificate` model.

### Models

- `Team`: Represents a team with fields for name, image, years of experience, stack, educational qualification, description, social media links, slug, and email.
- `Skill`: Represents a skill with fields for name and team.
- `Certificate`: Represents a certificate with fields for name and team.

### Example Requests

```bash
# List all teams
curl -X GET http://myapi.nanocodes.com.ng/teams/team

# Retrieve details of a specific team
curl -X GET http://myapi.nanocodes.com.ng/teams/team/1/

# Get teams by stack
curl -X GET http://myapi.nanocodes.com.ng/teams/get_teams_by_stack/ui-ux

# Get skills by team
curl -X GET http://myapi.nanocodes.com.ng/teams/get_skills_by_team/1

# Get certificates by team
curl -X GET http://myapi.nanocodes.com.ng/teams/get_certificate_by_team/1

# Get teams by tag
curl -X GET http://myapi.nanocodes.com.ng/teams/get_team_by_tag/1
```

### Example Responses

```json
// Example response for TeamsViewSet
[
    {
        "id": 1,
        "name": "Team A",
        "image": "http://example.com/image.jpg",
        "years_of_experience": 5,
        "stack": "ui-ux",
        "educational_qualification": "Bachelor's Degree in UI/UX Design",
        "description": "We are a team of UI/UX designers.",
        "twitter_link": "http://twitter.com/team_a",
        "instagram_link": "http://instagram.com/team_a",
        "facebook_link": "http://facebook.com/team_a",
        "linkedln_link": "http://linkedin.com/team_a",
        "slug": "team-a",
        "email": "team_a@example.com"
    },
    // ... more teams
]

// Example response for GetTeamsByStackViewSet, GetSkillByTeamViewSet, GetCertificatesByTeamViewSet, and GetTeamByTagViewSet
// will be similar to the TeamsViewSet response
```

Note: The `Skill` and `Certificate` models are not fully defined in the provided code snippet, so the serializers and views related to these models are not fully documented. You would need to provide the full code for these models and serializers to get a complete API documentation.