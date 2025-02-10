# Using Date, Time and Timestamp in Ansible Playbook

Welcome to another episode of Ansible Pilot! I'm Luca Berton, and today we're diving into the fascinating world of handling date, time, and timestamps in Ansible Playbooks. We'll explore the `ansible_date_time` variable, conduct a live Playbook, and provide you with simple Ansible code to get started.

<iframe width="560" height="315"
src="https://www.youtube.com/embed/toK9Fr_d9AA"
frameborder="0" allowfullscreen>
</iframe>

## The `ansible_date_time` Variable

Ansible simplifies working with date and time information through the `ansible_date_time` variable. This built-in variable comes packed with a wealth of information, neatly organized into key-value pairs. Let's take a closer look at some of the key values it provides:

```yaml
"ansible_date_time": {
    "date": "2022-05-18",
    "day": "18",
    "epoch": "1652887408",
    "hour": "15",
    "iso8601": "2022-05-18T15:23:28Z",
    "minute": "23",
    "month": "05",
    "second": "28",
    "time": "15:23:28",
    "tz": "UTC",
    "weekday": "Wednesday",
    "weekday_number": "3",
    "year": "2022"
}
```

These values cover everything from the current date, time, and timezone to more detailed information like the day of the week, month, and year. This data can be immensely useful in various scenarios within your Ansible Playbook.

One important note: to leverage the `ansible_date_time` variable, ensure that Ansible Facts are enabled in your playbook by including `gather_facts: true`.

## Playbook

Are you ready for a hands-on experience? Let's jump into a quick live Playbook where we'll showcase how to display the full `ansible_date_time` and the ISO8601 format.

### Ansible Playbook Code

```yaml
---
- name: date and time Playbook
  hosts: all
  gather_facts: true
  tasks:
    - name: date and time
      ansible.builtin.debug:
        var: ansible_date_time
    - name: ISO8601
      ansible.builtin.debug:
        var: ansible_date_time.iso8601
```

{{< promote-video-book >}}

### Execution

Run the following command to execute the playbook:

```bash
$ ansible-playbook -i inventory datetime_fact.yml
```

The output will provide detailed information about the current date and time, as well as the ISO8601 format.

## Conclusion

Congratulations! You've just learned how to harness the power of date, time, and timestamp variables in your Ansible Playbooks. The `ansible_date_time` variable opens up a world of possibilities for managing time-related data effortlessly. Feel free to explore and integrate this knowledge into your automation workflows.
Happy automating!