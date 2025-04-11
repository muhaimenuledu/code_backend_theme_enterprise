/** @odoo-module **/

import { NavBar } from '@web/webclient/navbar/navbar';
import { patch } from "@web/core/utils/patch";

import { onMounted, useRef, onWillUnmount } from "@odoo/owl";

patch(NavBar.prototype, {
    setup() {
        super.setup();

        this.openElement = useRef("openSidebar");
        this.closeElement = useRef("closeSidebar");
        this.topHeading = useRef("sidebar_icon");
        this.sidebarLinks = useRef("sidebarLinks");

        this.sidebarLinkHandler = this.handleSidebarLinkClick.bind(this);
        this.openSidebarHandler = this.openSidebar.bind(this);
        this.closeSidebarHandler = this.closeSidebar.bind(this);

        onMounted(() => {
            this.addEventListeners();
        });

        onWillUnmount(() => {
            this.removeEventListeners();
        });
    },

    addEventListeners() {
        const openSidebarElement = this.openElement?.el;
        const closeSidebarElement = this.closeElement?.el;
        const sidebarLinkElements = this.sidebarLinks?.el?.children;

        if (sidebarLinkElements) {
            Array.from(sidebarLinkElements).forEach(link => {
                link.addEventListener('click', this.sidebarLinkHandler);
            });
        }
        if (openSidebarElement) {
            openSidebarElement.addEventListener('click', this.openSidebarHandler);
        }
        if (closeSidebarElement) {
            closeSidebarElement.addEventListener('click', this.closeSidebarHandler);
        }
    },

    removeEventListeners() {
        const openSidebarElement = this.openElement?.el;
        const closeSidebarElement = this.closeElement?.el;
        const sidebarLinkElements = this.sidebarLinks?.el?.children;

        if (sidebarLinkElements) {
            Array.from(sidebarLinkElements).forEach(link => {
                link.removeEventListener('click', this.sidebarLinkHandler);
            });
        }
        if (openSidebarElement) {
            openSidebarElement.removeEventListener('click', this.openSidebarHandler);
        }
        if (closeSidebarElement) {
            closeSidebarElement.removeEventListener('click', this.closeSidebarHandler);
        }
    },

    openSidebar() {
        const rootElement = this.root?.el?.nextElementSibling;
        if (rootElement) {
            rootElement.style.marginLeft = '200px';
            rootElement.style.transition = 'all .1s linear';
        }

        this.openElement?.el?.style.setProperty('display', 'none');
        this.closeElement?.el?.style.setProperty('display', 'block');

        if (this.root?.el?.lastChild?.nodeType === Node.ELEMENT_NODE) {
            this.root.el.lastChild.style.display = 'block';
        }

        if (this.topHeading?.el?.nodeType === Node.ELEMENT_NODE) {
            Object.assign(this.topHeading.el.style, {
                marginLeft: '200px',
                transition: 'all .1s linear',
                width: 'auto',
            });
        }
    },

    closeSidebar() {
        const rootElement = this.root?.el?.nextElementSibling;
        if (rootElement) {
            rootElement.style.marginLeft = '0px';
            rootElement.style.transition = 'all .1s linear';
        }

        this.openElement?.el?.style.setProperty('display', 'block');
        this.closeElement?.el?.style.setProperty('display', 'none');

        if (this.root?.el?.lastChild?.nodeType === Node.ELEMENT_NODE) {
            this.root.el.lastChild.style.display = 'none';
        }

        if (this.topHeading?.el?.nodeType === Node.ELEMENT_NODE) {
            Object.assign(this.topHeading.el.style, {
                marginLeft: '0px',
                width: 'auto',
            });
        }
    },

    handleSidebarLinkClick(event) {
        const closeSidebarElement = this.closeElement?.el;
        if (closeSidebarElement) closeSidebarElement.style.display = 'none';

        if (this.topHeading?.el?.nodeType === Node.ELEMENT_NODE) {
            Object.assign(this.topHeading.el.style, {
                marginLeft: '0px',
                width: '100%',
            });
        }

        const li = event.currentTarget;
        const a = li.firstElementChild;
        const id = a.getAttribute('data-id');
        if (id) {
            document.querySelector('header').className = id;
        }

        // Remove 'active' class from all links
        Array.from(this.sidebarLinks?.el?.children || []).forEach(li => {
            li.firstElementChild.classList.remove('active');
        });

        a.classList.add('active');
        this.closeSidebar();
    },
});
