# entrypoint

- name: Ensure .ssh directory exists.
  file:
    dest: "{{ dest_key | dirname }}"
    mode: 0700
    state: directory
  tags:
    - dotfiles
    - install
    - ssh
- name: Install ssh key
  copy:
    src: "{{ source_key }}"
    dest: "{{ dest_key }}"
    mode: 0600
  tags:
    - dotfiles
    - install
    - ssh
- name: Install ssh key public
  copy:
    src: "{{ source_key }}.pub"
    dest: "{{ dest_key }}.pub"
    mode: 0644
  tags:
    - dotfiles
    - install
    - ssh
- name: Set authorized key took from file
  authorized_key:
    user: "{{ lookup('env', 'USER') }}"
    state: present
    key: "{{ lookup('env', 'HOME') }}/.ssh/id_rsa.pub"
  with_fileglob:
  - "{{ lookup('env', 'HOME') }}/.ssh/*.pub"
