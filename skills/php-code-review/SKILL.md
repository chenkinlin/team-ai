---
name: php-code-review
description: Review PHP and ThinkPHP 5 code for security, authorization, data consistency, performance, reliability, and PHP compatibility. Use when the user asks for PHP code review, PR review, change inspection, or a security and quality audit of PHP code.
---

# PHP Code Review

## Project context

This project uses ThinkPHP 5.0.7 and tpadmin, with multiple
admin, api, and common modules.

It contains legacy PHP code and limited automated testing.
Review changes against the existing architecture rather
than imposing a complete rewrite.

Until the production PHP version is verified, use PHP 7.0
as a conservative syntax compatibility baseline.

## Review workflow

1. Identify the review scope:
   - User-specified files or methods, if provided
   - Otherwise, current Git diff against the appropriate base
   - If there is no diff, ask for or identify a relevant scope

2. Read the applicable project Rules and documentation.
   Inspect callers, dependencies, and existing conventions
   when they are relevant to the changes.

3. Review potential problems in these areas:

   Security:
   - SQL injection and unsafe dynamic identifiers
   - Hardcoded credentials or exposed sensitive information
   - Unsafe output rendering and XSS
   - Missing input validation

   Authentication and authorization:
   - Admin Session and RBAC checks
   - API v2 token and method-level authorization
   - Object-level permissions for branches, sites, users
     and business data

   Data consistency:
   - Missing or incorrect database transactions
   - Concurrent state transitions
   - Database, Redis, Kafka and Elasticsearch consistency
   - Idempotency, retries and partial failures

   Performance:
   - N+1 database queries
   - Unbounded queries and missing pagination
   - Excessive database access in loops
   - Repeated remote calls

   Reliability:
   - Empty catch blocks and swallowed errors
   - Queue duplicate processing or message loss
   - Redis expiration and cache invalidation
   - Long-running worker resource leaks

   Compatibility:
   - PHP 7.0 syntax compatibility
   - ThinkPHP 5.0.7 API compatibility
   - Existing endpoint behavior and response formats

4. Report only actionable findings supported by code evidence.
   Avoid speculative or generic findings without evidence.

5. Distinguish:
   - New problems introduced by this change
   - Existing problems in nearby legacy code

6. Do not modify code during a review unless explicitly asked.

## Finding format

For each finding, include:

- Severity: Critical / High / Medium / Low
- File and line number
- Problem
- Evidence and impact
- Recommended fix
- Whether it was introduced by this change or already existed

Never include actual secret values in findings.

## Final report

Return:

1. Review scope
2. Findings ordered by severity
3. Security and compatibility risks
4. Verification performed
5. Verification not performed
6. Overall review conclusion

If no actionable findings are discovered, say so explicitly,
but do not claim the code is guaranteed safe or correct.

Do not claim tests passed unless they actually ran.
Do not read or print the contents of sensitive .env files.
